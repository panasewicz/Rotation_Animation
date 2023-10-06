from PIL import Image
import matplotlib.pyplot as plt
from google.colab import files

uploaded = files.upload()

# Load the images
main_img = Image.open("Main.png")
layers = [Image.open(f"Layer_{i}.png") for i in range(1, 8)]
last_img = Image.open("Last.png")

# Define the number of frames and the rotation angle step
num_frames = 60
angle_step = 360 / num_frames

combined_frames = []

for i in range(num_frames):
    # Start with the main image as the base
    frame = main_img.copy()
    
    # Add the rotating layers
    for idx, layer in enumerate(layers):
        rotation_angle = i * angle_step if idx % 2 == 0 else -i * angle_step
        rotated_layer = layer.rotate(rotation_angle)
        paste_x = (frame.width - rotated_layer.width) // 2
        paste_y = (frame.height - rotated_layer.height) // 2
        frame.paste(rotated_layer, (paste_x, paste_y), rotated_layer)
    
    # Add the last static image
    paste_x = (frame.width - last_img.width) // 2
    paste_y = (frame.height - last_img.height) // 2
    frame.paste(last_img, (paste_x, paste_y), last_img)
    
    combined_frames.append(frame)

# Save the combined GIF
gif_path = "multi_layer_kaleidoscope_animation.gif"
combined_frames[0].save(
    gif_path, 
    save_all=True, 
    append_images=combined_frames[1:], 
    optimize=False, 
    duration=100, 
    loop=0
)

# Display the combined GIF to ensure it's working
with Image.open(gif_path) as gif_img:
    plt.imshow(gif_img)
    plt.axis('off')
    plt.show()


from google.colab import files
files.download(gif_path)
