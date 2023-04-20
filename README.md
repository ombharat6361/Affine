# Affine
def affine(img,ang=20,sx=0.5,tx=20):
    #Reading the image
    img = cv2.imread(img)
    img = cv2.cvtColor(img,cv2.COLOR_BGR2RGB)
    height,width = img.shape[:2]
    #Scaling
    M = np.float32([[Scx,0,0],[0,Scy,0]]) #1,1
    dst = cv2.warpAffine(img,M,(width,height))
    
    #Rotation
    R = cv2.getRotationMatrix2D(center=(width//2,height//2),angle=ang,scale=1)
    dst = cv2.warpAffine(img,R,(width,height))
    
    #Shearing
    M = np.float32([[1,sx,0],[sy,1,0]])
    dst = cv2.warpAffine(dst,M,(width,height))
    
    #Translation
    M = np.float32([[1,0,tx],[0,1,ty]])
    dst = cv2.warpAffine(dst,M,(width,height))
    
    return dst
 
