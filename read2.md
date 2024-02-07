import easyocr

def print_with_spacing_and_lines(image_path):
    reader = easyocr.Reader(['en'])  # Initialize EasyOCR with English language

    # Perform OCR
    result = reader.readtext(image_path)

    # Reconstruct lines and spacing
    reconstructed_text = ""
    for detection in result:
        text, _, _ = detection
        reconstructed_text += text + " "  # Add space between words

    # Print formatted text
    print(reconstructed_text)

# Example usage
image_path = 'example_image.jpg'
print_with_spacing_and_lines(image_path)

