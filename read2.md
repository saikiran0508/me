import easyocr
reader = easyocr.Reader(['en'])  # English language
result = reader.readtext('image_path.jpg')
result.sort(key=lambda x: x[0][1])
lines = []
current_line = []

for detection in result:
    text, bbox = detection[1], detection[0]
    if not current_line or abs(bbox[1] - current_line[-1][0][1]) < 20:  # Adjust the threshold as needed
        current_line.append((bbox, text))
    else:
        lines.append(current_line)
        current_line = [(bbox, text)]
if current_line:
    lines.append(current_line)
formatted_text = '\n'.join([' '.join([word[1] for word in line]) for line in lines])
print(formatted_text)
