### Async/await

С выходом в сентябре 2015 года Python 3.5 в нем появились ключевые слова async и await, здорово напоминающие соответствующую концепцию в C#. Метод, снабженный модификатором async, оборачивается в специальный объект awaitable, которого можно дожидаться с помощью await. В свою очередь await означает "здесь возможно переключение контекста выполнения  на другой контекст, выполняющийся в том же потоке (обратите внимание!)". При этом переключение может и не произойти (т. е. выполнение продолжится как ни в чем не бывало), это уж как карта ляжет.

Пример клиентского приложения:

```python
import aiohttp
import asyncio

async def fetch(session, url):
    async with session.get(url) as response:
        return await response.text()

async def main():
    async with aiohttp.ClientSession() as session:
        html = await fetch(session, 'http://python.org')
        print(html)

# Организуем вызов асинхронного вызова из синхронного
loop = asyncio.get_event_loop()
loop.run_until_complete(main())
```

Пример HTTP-сервера:

```python
from aiohttp import web

async def handle(request):
    name = request.match_info.get('name', "Anonymous")
    text = "Hello, " + name
    return web.Response(text=text)

app = web.Application()
app.add_routes([web.get('/', handle),
                web.get('/{name}', handle)])

web.run_app(app)
```

Пример TCP-клиента:

```python
import asyncio


async def tcp_echo_client(message, loop):
    reader, writer = await asyncio.open_connection('127.0.0.1', 8888,
                                                   loop=loop)

    print('Send: %r' % message)
    writer.write(message.encode())

    data = await reader.read(100)
    print('Received: %r' % data.decode())

    print('Close the socket')
    writer.close()


message = 'Hello World!'
loop = asyncio.get_event_loop()
loop.run_until_complete(tcp_echo_client(message, loop))
loop.close()
```

Пример TCP-сервера:

```python
import asyncio

async def handle_echo(reader, writer):
    data = await reader.read(100)
    message = data.decode()
    addr = writer.get_extra_info('peername')
    print("Received %r from %r" % (message, addr))

    print("Send: %r" % message)
    writer.write(data)
    await writer.drain()

    print("Close the client socket")
    writer.close()

loop = asyncio.get_event_loop()
coro = asyncio.start_server(handle_echo, '127.0.0.1', 8888, loop=loop)
server = loop.run_until_complete(coro)

# Serve requests until Ctrl+C is pressed
print('Serving on {}'.format(server.sockets[0].getsockname()))
try:
    loop.run_forever()
except KeyboardInterrupt:
    pass

# Close the server
server.close()
loop.run_until_complete(server.wait_closed())
loop.close()
```