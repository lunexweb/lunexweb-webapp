# Fonts Directory

This directory is for self-hosted fonts to optimize performance and reduce external dependencies.

## Inter Font

The project uses the Inter font family for optimal readability and modern aesthetics.

### How to Add Inter Font

1. **Download Inter Variable Font**
   - Visit: https://rsms.me/inter/
   - Download the variable font file: `Inter-roman.var.woff2`

2. **Place in this directory**
   - Rename to: `inter-var.woff2`
   - The CSS in `src/app.css` will automatically load it

3. **Alternative: Use Google Fonts**
   - If you prefer Google Fonts, update `src/app.css`:
   ```css
   /* Replace the @font-face with: */
   @import url('https://fonts.googleapis.com/css2?family=Inter:wght@100;200;300;400;500;600;700;800;900&display=swap');
   ```

### Font Weights Available

- 100 (Thin)
- 200 (Extra Light)
- 300 (Light)
- 400 (Regular)
- 500 (Medium)
- 600 (Semi Bold)
- 700 (Bold)
- 800 (Extra Bold)
- 900 (Black)

### Performance Benefits

- **Self-hosted**: No external requests
- **Variable font**: Single file for all weights
- **WOFF2 format**: Optimal compression
- **Font-display: swap**: Prevents layout shift 