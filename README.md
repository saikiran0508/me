from cryptography.hazmat.primitives.ciphers import Cipher, algorithms, modes
from cryptography.hazmat.backends import default_backend
from cryptography.hazmat.primitives import padding
import base64
import pandas as pd

# 16-byte (128-bit) key and IV — use a secure and consistent key for real use
key = b'mysecretaeskey16'
iv = b'fixedinitvector1'

# Encrypt function (AES-CBC with padding)
def encrypt_id(text):
    padder = padding.PKCS7(128).padder()
    padded_data = padder.update(text.encode()) + padder.finalize()

    cipher = Cipher(algorithms.AES(key), modes.CBC(iv), backend=default_backend())
    encryptor = cipher.encryptor()
    ct = encryptor.update(padded_data) + encryptor.finalize()

    return base64.urlsafe_b64encode(ct).decode()

# Decrypt function
def decrypt_id(enc_text):
    ct = base64.urlsafe_b64decode(enc_text.encode())

    cipher = Cipher(algorithms.AES(key), modes.CBC(iv), backend=default_backend())
    decryptor = cipher.decryptor()
    padded_data = decryptor.update(ct) + decryptor.finalize()

    unpadder = padding.PKCS7(128).unpadder()
    data = unpadder.update(padded_data) + unpadder.finalize()

    return data.decode()

# Example usage with pandas
df = pd.DataFrame({'id': ['C001', 'B002', 'C001', 'X999']})
df['encrypted_id'] = df['id'].apply(encrypt_id)
df['decrypted_id'] = df['encrypted_id'].apply(decrypt_id)

print(df)
