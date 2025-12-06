# Steganography
# 🖼️ Image Steganography Tool

A Python-based GUI application that allows you to hide secret messages within images and extract them later. This tool uses image steganography techniques to embed text data into image files without visibly altering the image.

## 📋 Table of Contents

- [Features](#features)
- [How It Works](#how-it-works)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Requirements](#requirements)
- [Supported Formats](#supported-formats)
- [Technical Details](#technical-details)
- [Contributing](#contributing)
- [License](#license)

## ✨ Features

- **Encode Messages**: Hide secret text messages within image files
- **Decode Messages**: Extract hidden messages from encoded images
- **User-Friendly GUI**: Intuitive Tkinter-based interface
- **Image Preview**: Visual preview of selected images
- **Multiple Format Support**: Works with PNG, JPEG, and JPG images
- **File Management**: Easy file selection and saving
- **Error Handling**: Robust error messages and validation
- **Lossless Encoding**: Hidden data embedded using LSB (Least Significant Bit) technique

## 🔐 How It Works

This application uses **Least Significant Bit (LSB) Steganography**:

### Encoding Process
1. Select an image to hide data in
2. Enter the secret message
3. The algorithm converts the message to binary
4. Each bit is embedded into the least significant bit of pixel color values
5. The modified image is saved with hidden data intact

### Decoding Process
1. Select an image with hidden data
2. The algorithm extracts bits from pixel LSBs
3. Bits are converted back to characters
4. The original hidden message is displayed

**Why LSB?** The least significant bit of pixel colors has minimal impact on visual perception, making the changes imperceptible to the human eye.

## 🚀 Installation

### Prerequisites
- Python 3.7 or higher
- pip (Python package manager)

### Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/image-steganography.git
   cd image-steganography
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

   Or manually install required packages:
   ```bash
   pip install Pillow
   ```

3. **Run the application**
   ```bash
   python STEGANOGRAPHY.py
   ```

## 📖 Usage

### Encoding a Message

1. Launch the application
2. Click the **"Encode"** button
3. Select an image file (PNG, JPEG, or JPG)
4. Preview of the image will be displayed
5. Enter your secret message in the text box
6. Click **"Encode"** to embed the message
7. Choose a location and filename to save the encoded image
8. Success message will confirm the encoding

### Decoding a Message

1. Launch the application
2. Click the **"Decode"** button
3. Select an image that contains hidden data
4. Preview of the image will be displayed
5. The hidden message will automatically be extracted and displayed
6. Click **"Cancel"** to return to the main menu

## 📁 Project Structure

```
image-steganography/
├── STEGANOGRAPHY.py    # Main application file
├── requirements.txt    # Python dependencies
├── README.md          # This file
└── .gitignore         # Git ignore file
```

## 📦 Requirements

- **tkinter**: GUI framework (usually included with Python)
- **Pillow (PIL)**: Image processing library

See `requirements.txt` for details.

## 🖼️ Supported Formats

- **PNG** (.png) - Recommended (lossless compression)
- **JPEG** (.jpeg) - Supported
- **JPG** (.jpg) - Supported

**Note:** PNG is recommended because JPEG uses lossy compression, which can damage embedded data during saving.

## 🔧 Technical Details

### Encoding Algorithm

The `modify_Pix()` function processes pixels in groups of 9 (3x3 pixels):

1. Converts message characters to 8-bit binary
2. For each bit in the binary representation:
   - If bit is '0' and pixel LSB is 1: subtract 1 from pixel value
   - If bit is '1' and pixel LSB is 0: subtract 1 from pixel value
3. Sets the last bit of the 9th pixel as an end marker

### Decoding Algorithm

The `decode()` function reverses the process:

1. Reads 9 pixels at a time
2. Extracts the LSB from the first 8 pixels to reconstruct a character
3. Converts binary to ASCII character
4. Continues until the end marker is found (odd LSB on 9th pixel)

### Data Capacity

The amount of text that can be hidden depends on image size:
- **Capacity** = (Image Width × Image Height) / 9 bytes
- Example: A 1920×1080 image can hide approximately 230 KB of text

## 🎨 GUI Components

- **Main Frame**: Welcome screen with Encode/Decode buttons
- **Encode Frame**: Image selection and message input
- **Decode Frame**: Image selection and hidden message display
- **Color Scheme**: Sky blue background with green action buttons and red cancel buttons

## 🐛 Known Limitations

- Large text messages may not fit in small images
- JPEG compression may corrupt embedded data
- Currently supports basic ASCII characters (full Unicode support can be added)
- Single-threaded GUI (large image processing may briefly freeze interface)

## 🔒 Security Note

This tool provides **obscurity, not encryption**. The hidden message is not encrypted, only hidden. For sensitive data, combine this with encryption before embedding.

## 💡 Possible Enhancements

- Add encryption layer for hidden messages
- Support for larger character sets (Unicode)
- Batch processing for multiple files
- Progress bar for large images
- Drag-and-drop file selection
- Command-line interface
- Multi-threaded processing
- Dark mode theme

## 🤝 Contributing

Contributions are welcome! Feel free to:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/YourFeature`)
3. Commit changes (`git commit -m 'Add your feature'`)
4. Push to the branch (`git push origin feature/YourFeature`)
5. Open a Pull Request

## 📝 License

This project is open source and available under the MIT License.

## 📧 Contact & Support

For issues, bugs, or feature requests, please open an issue on GitHub.

---

## 🎓 Educational Purposes

This tool is designed for educational purposes to understand:
- Image file formats and pixel manipulation
- LSB steganography technique
- Python GUI development with Tkinter
- Image processing with PIL/Pillow
- Binary data representation and manipulation

**Disclaimer:** Use this tool responsibly and legally. Ensure you have the right to hide data in images and respect privacy laws in your jurisdiction.

---

**Happy Steganography! Keep your secrets safe! 🔐**
