def modify_sas_script(input_file, output_file, path_changes):
    with open(input_file, 'r') as f:
        script_content = f.read()

    modified_content = script_content
    for old_path, new_path in path_changes:
        modified_content = modified_content.replace(old_path, new_path)

    with open(output_file, 'w') as f:
        f.write(modified_content)

# Example usage:
path_changes = [('/old/path1/', '/new/path1/'),
                ('/old/path2/', '/new/path2/')]

sas_scripts = ['script1.sas', 'script2.sas']  # List of SAS script files

for script in sas_scripts:
    modify_sas_script(script, f'modified_{script}', path_changes)
