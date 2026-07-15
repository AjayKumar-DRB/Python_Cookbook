# Unicode Reference

Python 3 strings are fully Unicode by default. While ASCII (0-127) is sufficient for most interview questions, some string questions involve wider Unicode concepts.

## 1. ord() and chr()
These work exactly the same for Unicode as they do for ASCII.

```python
ord('A') # 65
ord('ñ') # 241
ord('🚀') # 128640

chr(128640) # '🚀'
```

## 2. String Length
In Python 3, `len()` returns the number of Unicode code points, not the number of bytes.

```python
len("Hello") # 5
len("こんにちは") # 5 (Hiragana characters)
len("🚀") # 1
```

## 3. Checking Character Types
Python's built-in string methods handle Unicode cleanly.

```python
"123".isnumeric() # True
"١٢٣".isnumeric() # True (Arabic numerals)
"Ⅷ".isnumeric()  # True (Roman numeral 8)

"abc".isalpha() # True
"ñ".isalpha()   # True
```

## 4. Encoding and Decoding
If a problem explicitly asks you to deal with bytes (e.g., "Design a compression algorithm" or "Network serialization"):

```python
# String to Bytes
byte_data = "Hello".encode('utf-8')
print(byte_data) # b'Hello'

# Bytes to String
string_data = byte_data.decode('utf-8')
```
