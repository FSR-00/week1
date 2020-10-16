# day2


# Tuesday, 13 October 2020
# Professor Leon Tabak
# CSC355 Open Source Development
# Zhifei Xu


import numpy as np
from PIL import Image
from PIL import ImageDraw, ImageOps, ImageEnhance

def main():
    print( "Composite" )

    # replace this path with a path
    # that specifies the location of your image file
    photo = Image.open( r"/Users/xuzhifei/Desktop/image/1.jpg" )
    original_photo = photo.reduce(1)

    enhance_photo = ImageEnhance.Color(original_photo)
    enhance = enhance_photo.enhance(2)


    print("original_photo mode", original_photo.mode)
    print("original_photo size", original_photo.size)

    change_photo = ImageOps.grayscale(original_photo).convert("RGB")

    print("change_photo mode", change_photo.mode)
    print("change_photo size", change_photo.size)

    width, height = original_photo.size
    print( f'Photo measures {width} x {height} pixels' )

    mask_data = np.zeros((height, width), dtype=np.uint8)
    mask1_data = np.zeros((height, width), dtype=np.uint8)

    mask_data [  (height//2):, :]=255

    mask1_data[(width//2):, :]=255

    mask = Image.fromarray(mask_data, mode = "L")
    mask1 = Image.fromarray(mask1_data, mode="L")

    print("mask mode", mask.mode)
    print("mask size", mask.size)

    half_photo1 = Image.composite(enhance, original_photo, mask1)

    half_photo = Image.composite(half_photo1, change_photo, mask)
    draw =ImageDraw.Draw(half_photo)

    start1 = (0, height // 2)
    end1 = (width, height // 2)
    fill_color1 = (255, 99, 71)

    start2 = (0, height // 1.5)
    end2 = (width, height // 1.5)
    fill_color2 = (255, 245, 238)

    draw.line([start1, end1], fill= fill_color1, width=5)
    draw.line([start2, end2], fill=fill_color2, width=5)

    half_photo.show()



if __name__ == "__main__":
    main()
