from twilio.rest import Client
import requests
import io

# Twilio account credentials
account_sid = 'your_account_sid'
auth_token = 'your_auth_token'
client = Client(account_sid, auth_token)

# ASCII banner
banner = '''
    dMMMMb  .aMMMb  dMMMMb  dMMMMb  dMP dMMMMMMP 
   dMP.dMP dMP"dMP dMP"dMP dMP"dMP amr    dMP    
  dMMMMK" dMMMMMP dMMMMK" dMMMMK" dMP    dMP     
 dMP"AMF dMP dMP dMP.aMF dMP.aMF dMP    dMP      
dMP dMP dMP dMP dMMMMP" dMMMMP" dMP    dMP       
                                                 
    dMMMMb  dMP dMP .aMMMb  dMMMMb  dMMMMMP      
   dMP.dMP dMP dMP dMP"dMP dMP dMP dMP           
  dMMMMP" dMMMMMP dMP dMP dMP dMP dMMMP          
 dMP     dMP dMP dMP.aMP dMP dMP dMP             
dMP     dMP dMP  VMMMP" dMP dMP dMMMMMP          
                                                 

@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@.+@@@@@@@@@@@@@@@@@@@@@@@@@@@@+.%@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@%%..@@@@@@@@@@@@@@@@@@@@@@@@..@%%@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@+%@%.-%%@@@@@@@@@@@@@@@@@@=.%@@*%@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@%@-%%@@..%@%@@@@@@@@@@@@@@@..@@%@=%@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@.@@@%*..@@@@@@@@@@@@@@@@..+@@@@.@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@.%@@@@..-%@@@@@@@@@@@@@=..@@@%%.@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@##@%@@...#@@@@@@@@@@@@%. .%@%@*#@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@.-@@@...+@@@@@@@@@@@@.. .%@@=.@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@:#=+@...%*@@@@@@@@@@#....@*=*:@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@.-.%...%:*@@@@@@%@*... .#.-:@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@.-.....%-.-......-.-... ..:.@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@.:   ...          ...   :.@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@#.........     . ..:.... #@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@%@........      . ...... .@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@%@+.**...          ...#*.=@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@-@@.+.           ..+.%@:@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@%.#@%@*. ......... *@@%%.@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@%@..#=# .............#=#. @@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@**..:::...=-=-==....::..*+@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@.....:+..-..-=..-:.+....  %@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@:..:-.:*@@@%@@@@@@*:.--..-@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@=...%@@@@*=--=#+--=*@@@@.. =@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@+.@@@=@@@%=-=%+-=*@@@@*%@%.=@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@+=#@@%@%%*-+%@@@@@%%+@@@@@%@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@%:%*+-%@%@*-=%@%%#@%@+=*@@:@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@%@#:%-=-=+=-=%@%*=-==-=-%@-*@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@:#:@@+%@%+-+@%%%+*%@@+*@@.+-%@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@::%@@@@@@#=-=*%@=@*@@@@@@@.:@%@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@#-%-%%%@@@@@@#++===@#%%@@@%%@%%%-@%%@@@%@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@:...=@%@%@:.%@@@@%%#=@##%%@@@@:.@@%%%@..@:@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@%....:*.-@%%@%@+=-%@%@@@@@@@@%@-=@@@@@@@@:....:#@@@@@@@@@@@@@@
@@@@@@@@@@@@%:...+:     ..@@%:%%-%@#*##+=#%-%@+%@@@=*....     .@@@@@@@@@@@@@
@@@@@@@@@@@=..+=..      ....@@@@+=*@@@@@@@@@@@@@# #.... .     ..-@@@@@@@@@@@
@@@@@@@@%@:.....           ...-@@#%@@@@@%%#@@-. .....=..      .. .@@@@@@@@@@
@@@@@@@@@:*-....       .......=%@*#======+*%%=.......*:..  .....**:@@@@@@@@@
@@@@@@@@@@@+..::..........-@#=---=+------=*----#@..%.........:..@@@@@@@@@@@@
@@@@@@@@@@@*.+%@:#::....@@---=--=:=------=:-----=-@@.....-%:@**.*@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@%..@%*--=----=%@------+@#=-----==@@..#%@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
'''

print(banner)

# Function to send SMS
def send_sms(to_number, message, image_url=None):
    try:
        if image_url:
            # Send image as text message
            response = client.messages.create(
                body=message,
                from_='your_twilio_number',
                to=to_number,
                media_url=image_url
            )
        else:
            # Send plain text message
            response = client.messages.create(
                body=message,
                from_='your_twilio_number',
                to=to_number
            )
        print(f"Message sent to {to_number}")
    except Exception as e:
        print(f"Error sending message: {e}")

# Function to send image as text message
def send_image_as_text(to_number, image_url):
    try:
        # Download image from URL
        response = requests.get(image_url)
        image = Image.open(io.BytesIO(response.content))

        # Convert image to ASCII art
        ascii_art = convert_image_to_ascii(image)

        # Send ASCII art as text message
        send_sms(to_number, ascii_art)
    except Exception as e:
        print(f"Error sending image as text: {e}")

# Function to convert image to ASCII art
def convert_image_to_ascii(image, width=100):
    ascii_chars = [' ', '.', ':', '-', '=', '+', '*', '#', '%', '@']
    (old_width, old_height) = image.size
    aspect_ratio = float(old_height)/float(old_width)
    new_height = int(aspect_ratio * width)
    image = image.resize((width, new_height)).convert('L')
    pixels = image.getdata()
    ascii_art = ''.join(ascii_chars[pixel//25] for pixel in pixels)
    return ascii_art

# Main program loop
while True:
    print("1. Send SMS")
    print("2. Send Image as Text")
    print("3. Exit")

    choice = input("Enter your choice (1-3): ")

    if choice == '1':
        to_number = input("Enter the recipient's phone number (e.g. +1234567890): ")
        message = input("Enter the message: ")
        send_sms(to_number, message)
    elif choice == '2':
        to_number = input("Enter the recipient's phone number (e.g. +1234567890): ")
        image_url = input("Enter the image URL: ")
        send_image_as_text(to_number, image_url)
    elif choice == '3':
        print("Exiting...")
        break
    else:
        print("Invalid choice. Please try again.")
