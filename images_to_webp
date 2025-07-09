#!/bin/bash

# Check if ffmpeg is installed
if ! command -v ffmpeg &> /dev/null; then
    echo "Error: ffmpeg is not installed. Please install it first."
    exit 1
fi

# Set source and destination directories
SOURCE_DIR="${1:-./}"                # Default: current directory
DEST_DIR="${2:-$SOURCE_DIR/webp}"    # Default: source_dir/webp

# Create destination directory
mkdir -p "$DEST_DIR"

# Supported image extensions
extensions=("jpg" "jpeg" "png" "tiff" "bmp" "gif" "tif")

# Conversion settings
QUALITY=75            # Adjust quality (75-85 recommended)
SPEED=4               # Speed/quality tradeoff (0=slow/best, 6=fast/good)

# Convert images
for ext in "${extensions[@]}"; do
    find "$SOURCE_DIR" -maxdepth 1 -type f -iname "*.${ext}" | while read -r file; do
        filename=$(basename -- "$file")
        output="${DEST_DIR}/${filename%.*}.webp"
        
        echo "Converting: $filename → ${filename%.*}.webp"
        
        ffmpeg -v error -i "$file" \
            -vf "scale=iw:ih:flags=lanczos" \
            -compression_level 6 \
            -quality $QUALITY \
            -preset drawing \
            -speed $SPEED \
            "$output"
    done
done

echo "Conversion complete. WebP images saved to: $DEST_DIR"
