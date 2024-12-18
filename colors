import os



import random



import asyncio



import discord



from discord.ext import commands





# Bot setup



intents = discord.Intents.default()



intents.members = True  # Enables member-related events



bot = commands.Bot(command_prefix="!", intents=intents)





# Role name and color change interval



ROLE_NAME = "achievement grinder"



COLOR_CHANGE_INTERVAL = 3  # Change color every 3 seconds





# Event triggered when the bot is ready



@bot.event



async def on_ready():



    print(f"Logged in as {bot.user}")



    if not bot.guilds:



        print("The bot is not in any servers!")



    else:



        print(f"Connected to guild(s): {[guild.name for guild in bot.guilds]}")



    bot.loop.create_task(change_role_color())





# Function to change role color



async def change_role_color():



    await bot.wait_until_ready()  # Ensure the bot is ready before proceeding



    while True:



        for guild in bot.guilds:  # Loop through all guilds the bot is in



            role = discord.utils.get(guild.roles, name=ROLE_NAME)



            if role:



                new_color = discord.Color(random.randint(0, 0xFFFFFF))  # Generate random color



                try:



                    await role.edit(color=new_color)



                    print(f"Changed color of role '{ROLE_NAME}' in guild '{guild.name}' to {new_color}")



                except discord.Forbidden:



                    print(f"Permission denied to change role color in guild '{guild.name}'.")



                except discord.HTTPException as e:



                    print(f"HTTPException while editing role in guild '{guild.name}': {e}")



                except Exception as e:



                    print(f"Unexpected error in guild '{guild.name}': {e}")



            else:



                print(f"Role '{ROLE_NAME}' not found in guild '{guild.name}'.")



        await asyncio.sleep(COLOR_CHANGE_INTERVAL)  # Wait before the next change





# Run the bot using the token from environment variables



DISCORD_TOKEN = os.getenv("DISCORD_TOKEN")



if DISCORD_TOKEN:



    try:



        bot.run(DISCORD_TOKEN)



    except Exception as e:



        print(f"Error while starting the bot: {e}")



else:



    print("DISCORD_TOKEN environment variable not set.")
