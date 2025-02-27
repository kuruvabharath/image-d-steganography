# Image Steganography

This repository contains a Python script for performing image steganography using OpenCV. The script allows you to hide a secret message inside an image and retrieve it using a passcode.

## Features

- **Encrypting a Message:** Hide a secret message in an image.
- **Decrypting a Message:** Retrieve the hidden message using a passcode.

## Prerequisites

- Python (3.x)
- OpenCV (`cv2` library)
- A sample image (`mypic.jpg`)

## Installation

1. Clone the repository:
    ```bash
    git clone https://github.com/kuruvabharath/image-d-steganography.git
    cd image-d-steganography
    ```

2. Install the required libraries:
    ```bash
    pip install -r requirements.txt
    ```

## Usage

### Encrypting a Message

1. Run the script:
    ```bash
    python stego.py
    ```

2. Enter the secret message when prompted:
    ```
    Enter secret message: YourSecretMessage
    ```

3. Enter the passcode when prompted:
    ```
    Enter a passcode: YourPasscode
    ```

4. The script will encode the message into the image and save it as `encryptedImage.jpg`. The encrypted image will be opened automatically.

### Decrypting a Message

1. Run the script:
    ```bash
    python stego.py
    ```

2. Enter the passcode for decryption when prompted:
    ```
    Enter passcode for Decryption: YourPasscode
    ```

3. If the passcode is correct, the hidden message will be displayed. If the passcode is incorrect, an authentication failure message will be shown.

## Code Explanation

The script `stego.py` performs the following steps:

1. Reads the image:
    ```python
    img = cv2.imread("mypic.jpg")  # Replace with the correct image path
    ```

2. Gets the secret message and passcode from the user:
    ```python
    msg = input("Enter secret message:")
    password = input("Enter a passcode:")
    ```

3. Creates dictionaries to map characters to their ASCII values and vice versa:
    ```python
    d = {}
    c = {}
    for i in range(255):
        d[chr(i)] = i
        c[i] = chr(i)
    ```

4. Encodes the message into the image:
    ```python
    m = 0
    n = 0
    z = 0
    for i in range(len(msg)):
        img[n, m, z] = d[msg[i]]
        n = n + 1
        m = m + 1
        z = (z + 1) % 3
    cv2.imwrite("encryptedImage.jpg", img)
    os.system("start encryptedImage.jpg")  # Use 'start' to open the image on Windows
    ```

5. Initializes variables for decryption and gets the passcode for decryption:
    ```python
    message = ""
    n = 0
    m = 0
    z = 0
    pas = input("Enter passcode for Decryption")
    ```

6. Decodes the message from the image if the passcode is correct:
    ```python
    if password == pas:
        for i in range(len(msg)):
            message = message + c[img[n, m, z]]
            n = n + 1
            m = m + 1
            z = (z + 1) % 3
        print("Decryption message:", message)
    else:
        print("YOU ARE NOT auth")
    ```

## Notes

- Ensure that `mypic.jpg` is in the same directory as the script or provide the correct path to the image.
- The script assumes that the length of the secret message is less than or equal to the total number of pixels in the image.

Feel free to modify the script as needed for your specific use case.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

For any issues, please open an [issue](https://github.com/kuruvabharath/image-d-steganography/issues).