# DocuSwift - Beautiful File Converter

<div align="center">
  <img src="app_icon_placeholder.png" alt="DocuSwift Logo" width="120" height="120">
  
  <p>
    <strong>Easily convert your files to nearly any document format!</strong>
  </p>
  
  <p>
    <a href="#features">Features</a> •
    <a href="#supported-formats">Formats</a> •
    <a href="#architecture">Architecture</a> •
    <a href="#installation">Installation</a>
  </p>
</div>

---

## 🎯 Overview

DocuSwift is a modern, beautiful file converter app for iOS that makes file conversion simple and delightful. With support for dozens of file formats and both local and cloud-based conversion, DocuSwift is your go-to tool for all file conversion needs.

## ✨ Features

### 🚀 Fast & Easy Conversion
- **3-Step Process**: Select file → Choose format → Convert
- **Instant Local Conversions**: Many popular conversions happen locally in under a second
- **Cloud Conversions**: Advanced conversions processed on secure servers (usually < 15 seconds)

### 🎨 Beautiful Modern UI
- **Gradient-based Design**: Stunning blue-purple gradients throughout
- **Smooth Animations**: Spring-based animations for delightful interactions
- **Material Design**: Ultra-thin material cards with elegant shadows
- **Dark Mode Support**: Fully optimized for both light and dark modes

### 📁 Comprehensive Format Support
- **Documents**: DOC, DOCX, PDF, TXT, RTF, HTML, ODT, and more
- **Images**: JPG, PNG, HEIC, TIFF, BMP, SVG, and more
- **Ebooks**: EPUB, MOBI, AZW3, and more
- **Spreadsheets**: XLS, XLSX, CSV
- **Presentations**: PPT, PPTX, KEY

### 🔒 Privacy & Security
- **Local Processing**: Many conversions happen entirely on-device
- **Secure Cloud**: Cloud conversions use encrypted connections
- **Automatic Deletion**: Files immediately deleted from servers after conversion
- **No Data Collection**: Your files are never stored or analyzed

### 📱 Sharing & Integration
- **Share Anywhere**: AirDrop, Messages, Mail, and more
- **Files Integration**: Save directly to iCloud Drive or local storage
- **Quick Actions**: Open converted files in any compatible app

### 📊 Conversion History
- **Track All Conversions**: See your conversion history with timestamps
- **Quick Access**: Re-share or open previous conversions
- **Easy Management**: Clear history or delete individual items

## 📂 Supported Formats

### Input Formats (Import)

#### Documents
ABW, DJVU, DOC, DOCM, DOCX, DOT, DOTX, HTML, HWP, LWP, MD, ODT, PAGES, PDF, RST, RTF, SDW, TEXT, TXT, WPD, WPS, ZABW

#### Ebooks
AZW, AZW3, AZW4, CBC, CBR, CBZ, CHM, EPUB, FB2, HTM, HTMLZ, LIT, LRF, MOBI, PDB, PML, PRC, RB, SNB, TCR, TXTZ

#### Images
HEIC, JPG, JPEG, PNG, ICO, SVG, EPS, BMP, GIF, NEF, TIFF

#### Spreadsheets
CSV, XLS, XLSX

#### Presentations
PPT, PPTX, KEY, PDF

### Output Formats (Export)

| Format | Category | Local | Description |
|--------|----------|-------|-------------|
| **DOCX** | Documents | ❌ | Microsoft Word |
| **DOC** | Documents | ❌ | Word 97-2003 |
| **PDF** | Documents | ✅ | Portable Document |
| **RTF** | Documents | ✅ | Rich Text Format |
| **TXT** | Documents | ✅ | Plain Text |
| **HTML** | Documents | ✅ | Web Page |
| **ODT** | Documents | ❌ | OpenDocument |
| **JPG** | Images | ✅ | JPEG Image |
| **PNG** | Images | ✅ | PNG Image |
| **EPUB** | Ebooks | ❌ | eBook Format |
| **MOBI** | Ebooks | ❌ | Kindle Format |
| **XLSX** | Spreadsheets | ❌ | Excel Workbook |
| **CSV** | Spreadsheets | ✅ | CSV File |
| **PPTX** | Presentations | ❌ | PowerPoint |
| **KEY** | Presentations | ❌ | Keynote |

✅ = Instant local conversion | ❌ = Cloud conversion

## 🏗 Architecture

### Project Structure

```
DocuSwift/
├── App/
│   ├── DocuSwiftApp.swift          # App entry point
│   └── ContentView.swift            # Main tab view
├── Views/
│   ├── ConvertView.swift            # Main conversion interface
│   ├── HistoryView.swift            # Conversion history
│   ├── FormatPickerView.swift       # Format selection
│   ├── DocumentPicker.swift         # File picker
│   └── ShareSheet.swift             # Share sheet
├── Models/
│   └── Models.swift                 # Data models
├── Managers/
│   └── ConversionManager.swift      # Conversion logic
└── Resources/
    └── Assets.xcassets              # App assets
```

### Key Components

#### 1. ConversionManager
The heart of the app, managing:
- File selection and validation
- Local vs cloud conversion routing
- Conversion state management
- History tracking

```swift
@MainActor
class ConversionManager: ObservableObject {
    @Published var currentJob: ConversionJob?
    @Published var conversionHistory: [ConversionJob] = []
    
    func startConversion(file: ConversionFile, format: OutputFormat) async
    // ... conversion logic
}
```

#### 2. Local Converter
Handles on-device conversions:
- Image format conversions (JPG, PNG, PDF)
- Text document conversions
- PDF generation from images and text
- Instant processing with no network required

#### 3. Cloud Converter
Manages server-based conversions:
- Upload progress tracking
- Server-side processing
- Download with progress
- Error handling and retry logic

### Data Models

#### ConversionFile
```swift
struct ConversionFile: Identifiable {
    let url: URL
    let name: String
    let size: Int64
    let type: String
}
```

#### OutputFormat
```swift
struct OutputFormat: Identifiable {
    let name: String
    let fileExtension: String
    let category: FileCategory
    let isLocal: Bool
    let icon: String
}
```

#### ConversionStatus
```swift
enum ConversionStatus {
    case idle
    case uploading(progress: Double)
    case converting
    case downloading(progress: Double)
    case completed(URL)
    case failed(String)
}
```

## 🎨 UI/UX Design Principles

### Color Scheme
- **Primary Gradient**: Blue to Purple (`[.blue, .purple]`)
- **Success**: Green for completed conversions
- **Warning**: Orange for processing states
- **Error**: Red for failures
- **Background**: Light gradients with ultra-thin materials

### Typography
- **Titles**: SF Rounded Bold for friendly appearance
- **Body**: SF Pro for optimal readability
- **Captions**: Secondary color for hierarchy

### Animations
- **Spring-based**: Natural, physics-based animations
- **Response**: 0.3-0.4s for quick interactions
- **Damping**: 0.6-0.75 for slight bounce

### Layout
- **Spacing**: Consistent 12-24pt spacing
- **Corner Radius**: 12-20pt for modern feel
- **Shadows**: Subtle shadows for depth
- **Material**: Ultra-thin material for cards

## 📲 Installation

### Requirements
- iOS 17.0 or later
- Xcode 15.0 or later
- Swift 5.9 or later

### Setup Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/DocuSwift.git
   cd DocuSwift
   ```

2. **Open in Xcode**
   ```bash
   open DocuSwift.xcodeproj
   ```

3. **Configure Cloud Conversion** (Optional)
   - Add your conversion API endpoint in `CloudConverter.swift`
   - Update authentication if needed

4. **Build and Run**
   - Select your target device/simulator
   - Press `Cmd + R` to build and run

## 🔧 Configuration

### Adding New Output Formats

To add a new output format, update `Models.swift`:

```swift
OutputFormat(
    name: "Your Format",
    fileExtension: "ext",
    category: .documents,
    description: "Format Description",
    isLocal: false,  // true if conversion is local
    icon: "doc.fill"
)
```

### Implementing Local Conversions

Add conversion logic in `ConversionManager.swift`:

```swift
func canConvert(file: ConversionFile, to format: OutputFormat) -> Bool {
    // Check if local conversion is supported
}

func convert(file: ConversionFile, to format: OutputFormat) async throws -> URL {
    // Implement conversion logic
}
```

## 🚀 Performance

### Local Conversions
- **Image to PDF**: < 1 second
- **Text to PDF**: < 1 second
- **Image format changes**: < 0.5 seconds

### Cloud Conversions
- **Upload**: Depends on file size and connection
- **Processing**: Usually < 10 seconds
- **Download**: Depends on file size and connection
- **Total**: Typically 5-15 seconds

## 🔐 Privacy

DocuSwift takes your privacy seriously:

1. **Local First**: Conversions happen locally when possible
2. **Temporary Storage**: Cloud files deleted immediately after conversion
3. **No Analytics**: No user data or conversion data is collected
4. **Secure Transfer**: All network requests use HTTPS
5. **No Accounts**: No sign-up or authentication required

## 🛠 Technology Stack

- **Language**: Swift 5.9
- **UI Framework**: SwiftUI
- **Concurrency**: Swift Async/Await
- **Architecture**: MVVM with Managers
- **Dependencies**: None (uses native frameworks only)

### Apple Frameworks Used
- SwiftUI
- Foundation
- UniformTypeIdentifiers
- PDFKit
- UIKit (for interop)

## 📝 TODO / Future Enhancements

- [ ] Add batch conversion support
- [ ] Implement compression options
- [ ] Add quality settings for image conversions
- [ ] Support for video format conversions
- [ ] Audio format conversion
- [ ] Widget for quick conversions
- [ ] Shortcuts integration
- [ ] iCloud sync for conversion history
- [ ] Mac Catalyst version
- [ ] watchOS companion app

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments

- Apple for the amazing SwiftUI framework
- SF Symbols for beautiful iconography
- The iOS developer community for inspiration

## 📧 Contact

Dillon Hunt - [Your Email or GitHub Profile]

Project Link: [https://github.com/yourusername/DocuSwift](https://github.com/yourusername/DocuSwift)

---

<div align="center">
  Made with ❤️ and SwiftUI
</div>
