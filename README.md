# Steganography Lab (High School Visit)
**Course Host:** CYBR 1100 – Introduction to Cyber Security  
**Topic:** Hiding and revealing messages with `steghide`  
**Time:** ~25 minutes

---

## What is Steganography?
**Steganography** is the practice of hiding a message *in plain sight*, typically inside an innocent-looking file (like a photo, audio, or other media). Unlike **encryption** (which scrambles content), steganography conceals the *existence* of the message. It has been used throughout history—from ancient wax tablets and invisible inks to modern digital images.

**Modern uses:**
- Watermarking and copyright protection  
- Covert communication in high-risk environments  
- Security research and capture-the-flag challenges  
- (Caution) It can be misused—our focus is ethical, legal, and educational use only.

---

## What you’ll do today
1. Install `steghide` (Windows).
2. Download a ZIP of images that contain hidden messages.
3. Extract the first secret using a provided passphrase.
4. Follow clues to uncover **two more** hidden messages.
5. Create your own stego-image using a file from `clean_images`.


---

## Install `steghide` (Windows)
1. Go to the official/maintainer download page for **steghide** [*steghide download Windows*](https://steghide.sourceforge.net/download.php).  
2. Download the Windows binary and unzip it (or run the installer, if provided).  
3. Place `steghide.exe` somewhere convenient (e.g., `C:\Tools\steghide\`) and add that folder to your **PATH** *or* run it from that folder.

> **Check installation:** open **Command Prompt** (or PowerShell) and run:
```bash
steghide --version
```

## Get the lab files

Download steghide.zip from this repo and unzip it.

You should see:
```lua
steghide-lab/
  Embedded_Images/
    dock.jpg        <-- first stego image (start here)
    ...             <-- more images with clues
  Clean_Images/
    AquaFire.jpg
    Dock.jpg
    Eye.jpg
    ...
```

## Part A — Extract your first secret
We’ve hidden a message in images/dock.jpg. The passphrase is:

**s3cr3tw0rd**

Command (Windows CMD or PowerShell):
```bash
cd path\to\steghide-lab\images
steghide extract -sf dock.jpg -p s3cr3tw0rd
```
-sf = stego file you’re extracting from
-p = passphrase

If successful, steghide will create the embedded file in the current folder (e.g., note1.txt).
Open the extracted file and read your first clue.

Tip: If you want to choose a different output filename:
```bash
steghide extract -sf dock.jpg -p s3cr3tw0rd -xf mynote.txt
```

## Part B — Follow the trail (2 more secrets)

Your first clue points to another image in images/ and may hint at a new passphrase or extraction trick.
Repeat the process:
```bash
steghide extract -sf <next-image>.jpg
```

If a passphrase is required, steghide will prompt you. Try the clue you found.
You will uncover two additional hidden messages. Keep a simple log of:
- Which image you used
- The passphrase (if any)
- The file extracted
- The clue you discovered

## Part C — Make your own stego-image

- Pick any image from clean_images/ and hide a short text message (e.g., secret.txt) inside it.
- Create a tiny text file:
```bash
echo This is my hidden message. > secret.txt
```

- Embed it in a cover image:
```bash
steghide embed -cf clean.jpg -ef secret.txt -p mypass123 -sf stego.jpg
```

-cf = cover file (your clean image)
-ef = embedded file (the secret text)
-p = passphrase (choose your own)
-sf = stego file name to create (optional; otherwise it overwrites the cover image)

### Test extraction (proof it works):
```bash
steghide extract -sf campus_stego.jpg -p mypass123 -xf recovered.txt
type recovered.txt
```

Challenge: Instead of a .txt, try hiding a small .png or .pdf—just keep it tiny.
--- 
### Common commands (cheat sheet)
# Show version/help
steghide --version
steghide --help

# Extract (with passphrase inline)
steghide extract -sf dock.jpg -p s3cr3tw0rd

# Extract (prompt for passphrase, custom output file)
steghide extract -sf image.jpg -xf output.txt

# Embed with explicit output stego file
steghide embed -cf cover.jpg -ef secret.txt -p pass123 -sf stego.jpg

### Troubleshooting

“Command not found”: Open CMD/PowerShell in the folder where steghide.exe lives, or add that folder to your PATH.

“Could not extract any data”: Wrong file or wrong passphrase—re-read the clue.

“File too large”: Use a smaller secret file or a larger cover image.

Permissions: Avoid protected folders (e.g., C:\Program Files\). Work in your Documents folder.

### Ethics & Safety

Only hide/extract data in files you own or have permission to use. Don’t share passphrases or stego files beyond this activity. This lab is for learning and responsible digital citizenship.

### Deliverables (for the visit)

- The three extracted clues (copy their text into a single .txt or .docx).
- Your own stego image (e.g., campus_stego.jpg) and the passphrase (submit privately).
- A 2–3 sentence reflection: What surprised you about steganography? How might this be used for good/ill?

**Have fun—and think like a defender!**
