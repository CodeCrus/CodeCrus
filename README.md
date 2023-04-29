from PIL import Image, ImageDraw, ImageFont

# Create a blank image
width, height = 1200, 1800
poster = Image.new('RGB', (width, height), color='white')

# Load image of electrical shock
shock_image = Image.open('electric-shock-image.jpg')
shock_image = shock_image.resize((600, 600), resample=Image.BOX)

# Load font for text
font_title = ImageFont.truetype('arial.ttf', 72)
font_text = ImageFont.truetype('arial.ttf', 36)

# Create a draw object
draw = ImageDraw.Draw(poster)

# Draw the image of electrical shock
poster.paste(shock_image, (300, 100))

# Draw the title
title = 'Electrical Safety at Home'
title_width, title_height = draw.textsize(title, font=font_title)
x = (width - title_width) / 2
y = 750
draw.text((x, y), title, font=font_title, fill='black')

# Draw the subtitle
subtitle = 'Effects of Electrical Shock'
subtitle_width, subtitle_height = draw.textsize(subtitle, font=font_text)
x = (width - subtitle_width) / 2
y = 860
draw.text((x, y), subtitle, font=font_text, fill='black')

# Draw the bullet points
bullet_points = [
    'Electrical shock can cause burns, tingling, numbness, and muscle contractions',
    'It can also cause respiratory failure, cardiac arrest, and even death',
    'To prevent electrical shock, make sure your home electrical system is up to code',
    'Always unplug appliances before working on them, and keep them away from water',
    'Do not touch electrical wires or outlets with wet hands or feet',
    'If someone is experiencing electrical shock, do not touch them, turn off the power, and call for help'
]
bullet_point_spacing = 50
bullet_point_y = 950

for point in bullet_points:
    bullet_point_width, bullet_point_height = draw.textsize('• ' + point, font=font_text)
    x = 300
    draw.text((x, bullet_point_y), '• ' + point, font=font_text, fill='black')
    bullet_point_y += bullet_point_height + bullet_point_spacing

# Save the poster as a PNG file
poster.save('electrical-safety-poster.png')
