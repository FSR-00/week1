# week1



# Monday, 12 October 2020
# Professor Leon Tabak
# CSC355 Open Source Development
# Zhifei Xu


import numpy as np
from PIL import Image
from PIL import ImageEnhance
from PIL import ImageDraw
from PIL import ImageFont


def main():
    print( "Composite" )

    # replace this path with a path
    # that specifies the location of your image file
    original_photo = Image.open( "Laker.jpg" )
    new_photo = original_photo.reduce( 1)
    en = ImageEnhance.Color(new_photo)
    enhance_end = en.enhance(3)


    font = ImageFont.truetype("Baoli.ttc", 60)
    add_number = ImageDraw.Draw(enhance_end)
    add_number.text((300,-20), u"24", font=font, fill="yellow")
    add_number.text((230, 200), u"For Kobe", font=font, fill="white")
    # size of photo that shown

    original_width, original_height = original_photo.size
    print(f'Photo measures {original_width} x {original_height} pixels')
    new_width, new_height = enhance_end.size
    print( f'Photo measures {new_width} x {new_height} pixels' )

    draw = ImageDraw.Draw(original_photo)
    original_photo.show()
    enhance_end.show()

if __name__ == "__main__":
    main()
