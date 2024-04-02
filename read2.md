def modify_sas_script(input_file, output_file, old_path, new_path):
    with open(input_file, 'r') as f:
        script_content = f.read()

    modified_content = script_content.replace(old_path, new_path)

    with open(output_file, 'w') as f:
        f.write(modified_content)

# Example usage:
input_file = 'original_script.sas'
output_file = 'modified_script.sas'
old_path = '/old/path/'
new_path = '/new/path/'

modify_sas_script(input_file, output_file, old_path, new_path)
