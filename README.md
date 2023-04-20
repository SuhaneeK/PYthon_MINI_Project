# PYthon_MINI_Project
Color Detection
 # -*- coding: utf-8 -*-
"""
Created on Sat Jan  7 15:18:08 2023

@author: suhan
DETECTS RED , GREEN, BLUE
"""

import numpy as np
import cv2

webcam = cv2.VideoCapture(0)
while(1):
    _, imageFrame=webcam.read()
    hsvFrame = cv2.cvtColor(imageFrame, cv2.COLOR_BGR2HSV)
    
    red_lower =np.array([136,87,111], np.uint8)
    red_upper = np.array([180,255,255],np.uint8)
    red_mask = cv2.inRange(hsvFrame, red_lower, red_upper)
    
    green_lower =np.array([25,52,72], np.uint8)
    green_upper = np.array([102,255,255],np.uint8)
    green_mask = cv2.inRange(hsvFrame, green_lower, green_upper) 
    
    blue_lower =np.array([136,87,111], np.uint8)
    blue_upper = np.array([180,255,255],np.uint8)
    blue_mask = cv2.inRange(hsvFrame, blue_lower, blue_upper)
    
    kernel=np.ones((5,5),"uint8")
    red_mask= cv2.dilate(red_mask,kernel)
    res_red=cv2.bitwise_and(imageFrame,imageFrame,mask=red_mask)
    
    green_mask= cv2.dilate(green_mask,kernel)
    res_green=cv2.bitwise_and(imageFrame,imageFrame,mask=green_mask)
    
    blue_mask= cv2.dilate(blue_mask,kernel)
    res_blue=cv2.bitwise_and(imageFrame,imageFrame,mask=blue_mask)
    
    contours,hierarchy= cv2.findContours(red_mask,cv2.RETR_TREE,cv2.CHAIN_APPROX_SIMPLE)
    
    for pic, contour in enumerate(contours):
        area= cv2.contourArea(contour)
        if(area> 300):
            x,y,w,h =cv2.boundingRect(contour)
            imageFrame =cv2.rectangle(imageFrame,(x,y),
                                      (x+w,y+h),(0,0,255),2)
            
            cv2.putText(imageFrame,"Red Colour",(x,y),
                        cv2.FONT_HERSHEY_SIMPLEX,
                        1.0,(0,0,255))
            contours,hierarchy=cv2.findContours(green_mask,
                                                cv2.RETR_TREE,
                                                cv2.CHAIN_APPROX_SIMPLE)
    for pic, contour in enumerate(contours):
        area= cv2.contourArea(contour)
        if(area> 300):
            x,y,w,h =cv2.boundingRect(contour)
            imageFrame =cv2.rectangle(imageFrame,(x,y),
                                      (x+w,y+h),(0,255,0),2)
            
            cv2.putText(imageFrame,"Green Colour",(x,y),
                        cv2.FONT_HERSHEY_SIMPLEX,
                        1.0,(0,255,0))
    for pic, contour in enumerate(contours):
        area= cv2.contourArea(contour)
        if(area> 300):
            x,y,w,h =cv2.boundingRect(contour)
            imageFrame =cv2.rectangle(imageFrame,(x,y),
                                      (x+w,y+h),(255,0,0),2)
            
            cv2.putText(imageFrame,"Blue Colour",(x,y),
                        cv2.FONT_HERSHEY_SIMPLEX,
                        1.0,(255,0,0))
    #porgram termination 
    cv2.imshow("Multiple Colour Detection in REal Time",imageFrame)
    if cv2.waitKey(10) & 0xFF ==ord('q'):
        webcam.release()
        cv2.destroyALLWindows()
        break
        
"""
DETECTS RED,GREEN,YELLOW
"""
import numpy as np
import cv2

webcam = cv2.VideoCapture(0)
while(1):
    _, imageFrame=webcam.read()
    hsvFrame = cv2.cvtColor(imageFrame, cv2.COLOR_BGR2HSV)
    
    red_lower =np.array([136,87,111], np.uint8)
    red_upper = np.array([180,255,255],np.uint8)
    red_mask = cv2.inRange(hsvFrame, red_lower, red_upper)
    
    green_lower =np.array([25,52,72], np.uint8)
    green_upper = np.array([102,255,255],np.uint8)
    green_mask = cv2.inRange(hsvFrame, green_lower, green_upper) 
    
    yellow_lower =np.array([112, 100, 100], np.uint8)
    yellow_upper = np.array([124, 255, 255],np.uint8)
    yellow_mask = cv2.inRange(hsvFrame, yellow_lower, yellow_upper)
    
    kernel=np.ones((5,5),"uint8")
    red_mask= cv2.dilate(red_mask,kernel)
    res_red=cv2.bitwise_and(imageFrame,imageFrame,mask=red_mask)
    
    green_mask= cv2.dilate(green_mask,kernel)
    res_green=cv2.bitwise_and(imageFrame,imageFrame,mask=green_mask)
    
    yellow_mask= cv2.dilate(yellow_mask,kernel)
    res_yellow=cv2.bitwise_and(imageFrame,imageFrame,mask=yellow_mask)
    
    contours,hierarchy= cv2.findContours(red_mask,cv2.RETR_TREE,cv2.CHAIN_APPROX_SIMPLE)
    
    for pic, contour in enumerate(contours):
        area= cv2.contourArea(contour)
        if(area> 300):
            x,y,w,h =cv2.boundingRect(contour)
            imageFrame =cv2.rectangle(imageFrame,(x,y),
                                      (x+w,y+h),(0,0,255),2)
            
            cv2.putText(imageFrame,"Red Colour=STOP!",(x,y),
                        cv2.FONT_HERSHEY_SIMPLEX,
                        1.0,(0,0,255))
            contours,hierarchy=cv2.findContours(red_mask,
                                                cv2.RETR_TREE,
                                                cv2.CHAIN_APPROX_SIMPLE)
    for pic, contour in enumerate(contours):
        area= cv2.contourArea(contour)
        if(area> 300):
            x,y,w,h =cv2.boundingRect(contour)
            imageFrame =cv2.rectangle(imageFrame,(x,y),
                                      (x+w,y+h),(0,255,0),2)
            
            cv2.putText(imageFrame,"Green Colour=GO GO!",(x,y),
                        cv2.FONT_HERSHEY_SIMPLEX,
                        1.0,(0,255,0))
            contours,hierarchy=cv2.findContours(green_mask,
                                                cv2.RETR_TREE,
                                                cv2.CHAIN_APPROX_SIMPLE)
    for pic, contour in enumerate(contours):
        area= cv2.contourArea(contour)
        if(area> 300):
            x,y,w,h =cv2.boundingRect(contour)
            imageFrame =cv2.rectangle(imageFrame,(x,y),
                                      (x+w,y+h),(0,255,255),2)
            
            cv2.putText(imageFrame,"Yellow Colour=BE READY!",(x,y),
                        cv2.FONT_HERSHEY_SIMPLEX,
                        1.0,(0,255,255))
            contours,hierarchy=cv2.findContours(yellow_mask,
                                                cv2.RETR_TREE,
                                                cv2.CHAIN_APPROX_SIMPLE)
    #porgram termination 
    cv2.imshow("Multiple Colour Detection in REal Time",imageFrame)
    if cv2.waitKey(10) & 0xFF ==ord('q'):
        webcam.release()
        cv2.destroyALLWindows()
        break
