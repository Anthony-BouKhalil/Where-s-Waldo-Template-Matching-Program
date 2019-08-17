setMediaPath(r"D:/")
waldo = makePicture('waldo.jpg')
scene = makePicture('scene.jpg')
tinyscene = makePicture('tinyscene.jpg')
tinywaldo = makePicture('tinywaldo.jpg')


tempW = getWidth(tinywaldo)
tempH = getHeight(tinywaldo)
searchW = getWidth(tinyscene)
searchH = getHeight(tinyscene)
BIG = 1000000
matrix = [[BIG for i in range(searchW)] for j in range(searchH)]
#minVal = 0
  
def compareOne(searchImage, template, x1, y1) :
  searchW = getWidth(searchImage)
  searchH = getHeight(searchImage)
  tempW = getWidth(template)
  tempH = getHeight(template)
  limitX = searchW - tempW 
  limitY = searchH - tempH
  sum = 0
  
      
  if x1 < limitX or y1 < limitY :  
    i = -1
    m = -1
        
    for y in range(y1, (y1 + tempH)) :
      i = i + 1
      m = m + 1
      k = -1
      for x in range(x1, (x1 + tempW)) :
        k = k + 1
        i = i + 1
        #print k
        pixelSearch = getPixel(searchImage, x, y)
        pixelTemp = getPixel(template, k, m)
        L2 = int(getRed(pixelTemp) + getGreen(pixelTemp) + getBlue(pixelTemp)) / 3
        grayScaleTemp = makeColor(L2, L2, L2)
        setColor(pixelTemp, grayScaleTemp)
        
        L = int(getRed(pixelSearch) + getGreen(pixelSearch) + getBlue(pixelSearch)) / 3
        grayScaleSearch = makeColor(L, L, L)
        setColor(pixelSearch, grayScaleSearch)
        sum = sum + abs(L-L2)
    
    if sum < minVal :
      minVal = sum 
      global minVal
      #print minVal
      minrow = y1
      global minrow
      mincol = x1
      global mincol
      
    #print sum
    #print 'after check', minVal
 
  matrix[y1][x1] = sum
    
        
def compareAll(template, searchImage) :
  tempW = getWidth(template)
  tempH = getHeight(template)
  searchW = getWidth(searchImage)
  searchH = getHeight(searchImage)
  limitX = searchW - tempW 
  limitY = searchH - tempH
  list1 = []
  list2 = []
  ans = []

  for y1 in range(limitY) :
   #print y1, 'out of', searchH  
    for x1 in range(limitX) :
    # print x1, 'out of', searchW     :
      compareOne(searchImage, template, x1, y1)
  return matrix

def find2Dmin(matrix) :
  compareAll(tinywaldo, tinyscene)
  print 'minVal', minVal
  print 'minrow', minrow
  print 'mincol', mincol


def displayMatch(searchImage, x1, y1, w1, h1, color) :
  grayscale(searchImage)

  addRect(tinyscene, x1, y1, tempW, tempH, blue)
  addRect(tinyscene, x1 - 1, y1 + 1, tempW, tempH, blue)
  addRect(tinyscene, x1 - 2, y1 + 2, tempW, tempH, blue)
  explore(searchImage)

  
def grayscale(picture) :
  for pixel in getPixels(picture) :
    L = (getRed(pixel) + getGreen(pixel) + getBlue(pixel)) / 3
    grayScale = makeColor(L, L, L)
    setColor(pixel, grayScale)

#Takes about 10 minutes on my computer for the function to finish and then the picture will appear 
def findWaldo(targetJPG, searchJPG) :
  compareAll(targetJPG, searchJPG)
  displayMatch(searchJPG, mincol, minrow, tempW, tempH, blue)