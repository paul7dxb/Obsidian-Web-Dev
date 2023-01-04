Used for dealing with images

- Image uploads
- Image upload resizing

# Installation

Library for working with images in Python

```
pip install pillow
```

# Resizing uploaded images

- Override save method in model
	- Open app's models.py

```python
def save(self, *args, **kwargs):
	super().save(*args, **kwargs) #Run parents save method
	#open profile image
	img = Image.open(self.image.path)
	#Resize image
	if img.height > 300 or img.width > 300:
		output_size = (300,300)
		img.thumbnail(output_size)
		img.save(self.image.path)
```