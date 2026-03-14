# zenn-lookup
import os
import requests

# COLORS
red = "\033[91m"
green = "\033[92m"
yellow = "\033[93m"
cyan = "\033[96m"
reset = "\033[0m"


def clear():
    os.system("clear" if os.name == "posix" else "cls")


def banner():
    print(cyan + r"""
███████╗███████╗███╗   ██╗███╗   ██╗
╚══███╔╝██╔════╝████╗  ██║████╗  ██║
  ███╔╝ █████╗  ██╔██╗ ██║██╔██╗ ██║
 ███╔╝  ██╔══╝  ██║╚██╗██║██║╚██╗██║
███████╗███████╗██║ ╚████║██║ ╚████║
╚══════╝╚══════╝╚═╝  ╚═══╝╚═╝  ╚═══╝

██╗      ██████╗  ██████╗ ██╗  ██╗██╗   ██╗██████╗
██║     ██╔═══██╗██╔═══██╗██║ ██╔╝██║   ██║██╔══██╗
██║     ██║   ██║██║   ██║█████╔╝ ██║   ██║██████╔╝
██║     ██║   ██║██║   ██║██╔═██╗ ██║   ██║██╔═══╝
███████╗╚██████╔╝╚██████╔╝██║  ██╗╚██████╔╝██║
╚══════╝ ╚═════╝  ╚═════╝ ╚═╝  ╚═╝ ╚═════╝ ╚═╝
""" + reset)

    print(yellow + " Created By ZennTech\n" + reset)

    print(red + "[01]" + yellow + " My IP")
    print(red + "[02]" + yellow + " Track IP")
    print(red + "[00]" + yellow + " Exit\n")

    print(cyan + " Inspo: HTR-TECH\n" + reset)


def get_my_ip():
    try:
        ip = requests.get("https://api.ipify.org").text
        print(green + f"\nYour IP: {ip}\n" + reset)
    except:
        print(red + "Error getting IP\n")


def track_ip():
    ip = input(green + "\nEnter IP: " + reset)

    try:
        r = requests.get(f"http://ip-api.com/json/{ip}")
        data = r.json()

        lat = data.get("lat")
        lon = data.get("lon")

        maps = f"https://www.google.com/maps?q={lat},{lon}"

        print(cyan + "\nIP Information\n" + reset)
        print("IP:", data.get("query"))
        print("Country:", data.get("country"))
        print("Region:", data.get("regionName"))
        print("City:", data.get("city"))
        print("ISP:", data.get("isp"))
        print("Maps:", maps)
        print()

    except:
        print(red + "Lookup failed\n")


while True:

    clear()
    banner()

    choice = input(green + "[~] Select An Option : " + reset)

    if choice in ["1", "01"]:
        clear()
        banner()
        get_my_ip()
        input("Press Enter...")

    elif choice in ["2", "02"]:
        clear()
        banner()
        track_ip()
        input("Press Enter...")

    elif choice in ["0", "00"]:
        print(red + "\nExiting...\n")
        break

    else:
        print(red + "Invalid option\n")
