from Crypto.Cipher import AES
import base64
import pandas as pd
from Crypto.Util.Padding import pad, unpad

# 16-byte (128-bit) key (must be fixed and securely stored)
key = b'my16bytefixedkey'

# AES encryption with ECB mode (deterministic and shorter output)
def encrypt_id(text):
    cipher = AES.new(key, AES.MODE_ECB)
    padded = pad(text.encode(), AES.block_size)
    encrypted = cipher.encrypt(padded)
    return base64.urlsafe_b64encode(encrypted).decode()

def decrypt_id(enc_text):
    cipher = AES.new(key, AES.MODE_ECB)
    decrypted = cipher.decrypt(base64.urlsafe_b64decode(enc_text.encode()))
    return unpad(decrypted, AES.block_size).decode()

# Example DataFrame
df = pd.DataFrame({'id': ['C001', 'C002', 'C001', 'B123']})
df['encrypted_id'] = df['id'].apply(encrypt_id)
df['decrypted_id'] = df['encrypted_id'].apply(decrypt_id)

print(df)
