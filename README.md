from cryptography.fernet import Fernet
import pandas as pd

# Load or generate your Fernet key (generate once and save it securely)
# key = Fernet.generate_key()
# Store this key safely and reuse it
key = b'your-previously-generated-key'  # replace with your actual key
fernet = Fernet(key)

# Sample DataFrame
df = pd.DataFrame({'id': ['C001', 'C002', 'C001', 'B123', 'C002']})

# Cache to store original → encrypted ID mapping
encrypt_cache = {}

# Encrypt function with caching
def encrypt_id(x):
    if x not in encrypt_cache:
        encrypted = fernet.encrypt(x.encode()).decode()
        encrypt_cache[x] = encrypted
    return encrypt_cache[x]

# Decrypt function
def decrypt_id(x):
    try:
        return fernet.decrypt(x.encode()).decode()
    except Exception:
        return x  # return as-is if not encrypted

# Apply encryption
df['encrypted_id'] = df['id'].apply(encrypt_id)

# Apply decryption (optional check)
df['decrypted_id'] = df['encrypted_id'].apply(decrypt_id)

print(df)
