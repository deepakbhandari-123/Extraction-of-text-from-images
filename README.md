# Extraction-of-text-from-images



import cv2
import os,argparse
import pytesseract
from PIL import Image

pytesseract.pytesseract.tesseract_cmd = 'C:\\Program Files (x86)\\Tesseract-OCR\\tesseract.exe'

for file in os.listdir("Pic3.png"):
    print('Iam here ...')
    if file.endswith(".png"):
        file_path = "Pic3.png" + str(file)
        print(file_path)
        images=cv2.imread(file_path)
        
        gray=cv2.cvtColor(images, cv2.COLOR_BGR2GRAY)
        
        cv2.threshold(gray, 0,255,cv2.THRESH_BINARY| cv2.THRESH_OTSU)[1]
        cv2.medianBlur(gray, 3)
        filename = "{}.jpg".format(os.getpid())
        cv2.imwrite(filename, gray)
        text = pytesseract.image_to_string(Image.open(filename))
        os.remove(filename)
        print(text)
        cv2.imshow("Image Input", images)
        cv2.imshow("Output In Grayscale", gray)
        cv2.waitKey(0)
        text_file_name = "ab" + str(file[:-4]) + "-Scanned.txt" 
        with open(text_file_name, "a") as f:
            f.write(text + "\n")
        


          
