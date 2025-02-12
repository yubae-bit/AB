# AB
Code for valentines card for my bb

library(ggplot2)
library(jpeg)
library(grid)

# Define heart shape using parametric equations
t <- seq(0, 2 * pi, length.out = 300)
heart <- data.frame(
  x = 16 * sin(t)^3,
  y = 13 * cos(t) - 5 * cos(2*t) - 2 * cos(3*t) - cos(4*t)
)

# Download and load the image from GitHub
img_path <- tempfile(fileext = ".jpg")
download.file("https://raw.githubusercontent.com/yubae-bit/AB/main/YDNO0210.JPG", img_path, mode = "wb")
img_raster <- rasterGrob(readJPEG(img_path), width = unit(8, "cm"), height = unit(8, "cm"))

# Create the 2D heart plot with the image centered inside
ggplot() +
  geom_polygon(data = heart, aes(x, y), fill = "red", color = "black") +  
  annotation_custom(img_raster, xmin = -6, xmax = 6, ymin = -4, ymax = 5) +  
  annotate("text", x = 0, y = 10, label = "Happy Valentine's Day!", size = 6, color = "black") +  
  annotate("text", x = 0, y = -12, label = "To: Annabae", size = 5, color = "black") +  
  theme_void()  

