# rov
import cv2
import numpy as np

frame = cv2.imread("sample.png")

"""# Image Blurring (Image Smoothing)
frame = cv2.GaussianBlur(img, (5, 5), 0)
# Convert BGR to HSV
hsv = cv2.cvtColor(frame, cv2.COLOR_BGR2HSV)
# define range of red color in HSV
low_red = np.array([150, 30, 30])
up_red = np.array([190, 255, 255])
# Threshold the HSV image to get only red colors
mask = cv2.inRange(hsv, low_red, up_red)
# Canny Edge deteciton
edges = cv2.Canny(mask, 100, 200)
lines = cv2.HoughLinesP(edges, 1, np.pi / 180, 50, maxLineGap=50)
for line in lines:
    x1, y1, x2, y2 = line[0]
    cv2.line(frame, (x1, y1), (x2, y2), (0, 255, 0), 5)"""
class linedetection:
	def __init__(self,x1,x2,y1,y2,slope,data):
		self.x1 = x1
		self.x2 = x2
		self.y1 = y1
		self.y2 = y2
		self.slope = slope
		self.data = []


	def slope(img):
		data = []

		frame = cv2.GaussianBlur(img, (5, 5), 0)

	# Convert BGR to HSV
		hsv = cv2.cvtColor(frame, cv2.COLOR_BGR2HSV)

	# define range of red color in HSV
		low_red = np.array([150, 30, 30])
		up_red = np.array([190, 255, 255])

	# Threshold the HSV image to get only red colors
		mask = cv2.inRange(hsv, low_red, up_red)
	# Canny Edge deteciton
		edges = cv2.Canny(mask, 100, 200)

		lines = cv2.HoughLinesP(edges, 1, np.pi / 180, 50, maxLineGap=50)

		for line in lines:
			x1, y1, x2, y2 = line[0]
			if x1 != x2:
				slope = (y2-y1) / (x2-x1)
				slope = round(slope, 3)


			data.append(slope)

		return data


print (linedetection.slope(frame))
cv2.imshow("frame", frame)
cv2.waitKey()
cv2.destroyAllWindows()
