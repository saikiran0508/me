from cryptography.fernet import Fernet

# Generate a key for encryption
key = Fernet.generate_key()
fernet = Fernet(key)

# Encrypt the password
password = "my_secret_password"
encrypted_password = fernet.encrypt(password.encode())

# Decrypt the password
decrypted_password = fernet.decrypt(encrypted_password).decode()

print(f"Key: {key}")
print(f"Encrypted password: {encrypted_password}")
print(f"Decrypted password: {decrypted_password}")
