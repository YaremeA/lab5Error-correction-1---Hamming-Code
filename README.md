def encode(message):
    # Convert each character to its ASCII value and then to an 8-bit binary string
    binary_sequence = ''.join(format(ord(char), '08b') for char in message)
    # Repeat each binary bit three times
    encoded_sequence = ''.join(bit * 3 for bit in binary_sequence)
    return encoded_sequence

def decode(encoded_sequence):
    # Split the encoded sequence into groups of three bits
    triplets = [encoded_sequence[i:i+3] for i in range(0, len(encoded_sequence), 3)]
    # Correct each triplet using majority voting
    corrected_bits = [
        '1' if triplet.count('1') > triplet.count('0') else '0'
        for triplet in triplets
    ]
    # Group the corrected bits into 8-bit binary sequences
    corrected_binary = ''.join(corrected_bits)
    # Convert each binary group back to characters
    decoded_characters = [
        chr(int(corrected_binary[i:i+8], 2))
        for i in range(0, len(corrected_binary), 8)
    ]
    # Return the decoded string
    return ''.join(decoded_characters)

# Example usage
input_text = "hello"
encoded_result = encode(input_text)
print("Encoded Message:", encoded_result)

decoded_result = decode(encoded_result)
print("Decoded Message:", decoded_result)
