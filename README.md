import random
from urllib import request
import discord
from discord.ext import commands
import os

print(os.listdir('images'))

intents = discord.Intents.default()
intents.message_content = True

bot = commands.Bot(command_prefix='$', intents=intents)

@bot.event
async def on_ready():
    print(f'We have logged in as {bot.user}')

@bot.command()
async def hello(ctx):
    await ctx.send(f'Привет! Я бот {bot.user}!')

@bot.command()
async def heh(ctx, count_heh = 5):
    await ctx.send("he" * count_heh)
@bot.command()
async def add(ctx, left: int, right: int):
    """Adds two numbers together."""
    await ctx.send(left + right)
@bot.command()
async def mem(ctx):
    img_name = random.choise(os.listdir('images'))
    with open(f'images/{img_name}', 'rb') as f:
            picture = discord.File(f)
   # Можем передавать файл как параметр!
    await ctx.send(file=picture)
@bot.command()
async def ani(ctx):
    img_name = random.choise(os.listdir('animals'))
    with open(f'animals/{img_name}', 'rb') as f:
            picture = discord.File(f)
   # Можем передавать файл как параметр!
    await ctx.send(file=picture)
@bot.command()
async def help():
    print(f'я могу делать это {bot.user}:')
    print(f'приветствие - $hello {bot.user}')
    print(f'делать heh много раз когда мне скажут - $heh {bot.user}')
    print(f'еще я могу складывать числа - $add {bot.user}')
    print(f'и функция - $help которая показывает что я могу {bot.user}')
def get_duck_image_url():    
    url = 'https://random-d.uk/api/random'
    res = request.get(url)
    data = res.json()
    return data['url']
bot.run("MTI3NzY5OTQ4NTA1MjQzNjQ4Mg.G0z1Bk.OLfw4lTMDG5rSPmVu0TLr7gH37tWU2tdWVBo5s")

