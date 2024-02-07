result.sort(key=lambda x: x[0][0][1])

# Process the result to maintain spacing and lines
lines = []
current_line = []

for detection in result:
    # Extract text and bounding box coordinates
    text, bbox = detection[1], detection[0]
    
    # Check if the current detection is in the same line as the previous
    if not current_line or abs(bbox[0][1] - current_line[-1][0][1]) < 20:  # Adjust the threshold as needed
        current_line.append((bbox, text))
    else:
        lines.append(current_line)
        current_line = [(bbox, text)]

# Append the last line
if current_line:
    lines.append(current_line)

# Format the extracted lines
formatted_text = '\n'.join([' '.join([word[1] for word in line]) for line in lines])

print(formatted_text)
