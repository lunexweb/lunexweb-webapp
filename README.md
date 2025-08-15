# LunexWeb Portfolio Website

A modern, responsive portfolio website built with SvelteKit, TailwindCSS, and GSAP animations. Inspired by the design aesthetic of Dennis Snellenberg's portfolio.

## 🚀 Features

- **Modern Design**: Clean, minimalist design with smooth animations
- **Responsive Layout**: Optimized for all devices and screen sizes
- **Smooth Scrolling**: Powered by Lenis for buttery-smooth scrolling
- **GSAP Animations**: Scroll-triggered animations and entrance effects
- **TailwindCSS**: Utility-first CSS framework for rapid development
- **TypeScript**: Full type safety throughout the application

## 🎨 Design System

### Colors
- **Primary Background**: `#F9FAFB` (Light gray)
- **Secondary Background**: `#E0D9D1` (Warm beige)
- **Footer Background**: `#000000` (Black)
- **Text**: `#000000` (Black on light backgrounds)
- **Text Light**: `#F9FAFB` (White on dark backgrounds)

### Typography
- **Font Family**: Inter (Variable font)
- **Weights**: 100-900

## 📱 Sections

1. **Hero Section**: Fullscreen introduction with main heading and CTA
2. **About Section**: Two-column layout with developer info and skills
3. **Services Section**: 4 service cards showcasing specialties
4. **Portfolio Section**: Grid of featured projects with filtering
5. **Contact Section**: Contact form and information
6. **Footer**: Social links and copyright information

## 🛠️ Technologies

- **Frontend Framework**: SvelteKit 2.0
- **Styling**: TailwindCSS 3.3
- **Animations**: GSAP 3.12 + ScrollTrigger
- **Smooth Scrolling**: Lenis 1.0
- **Language**: TypeScript
- **Build Tool**: Vite 5.0

## 🚀 Getting Started

### Prerequisites
- Node.js 18+ 
- npm or yarn

### Installation

1. Clone the repository
```bash
git clone <repository-url>
cd lunexweb-portfolio
```

2. Install dependencies
```bash
npm install
```

3. Start development server
```bash
npm run dev
```

4. Open your browser and navigate to `http://localhost:5173`

### Build for Production

```bash
npm run build
npm run preview
```

## 📁 Project Structure

```
src/
├── app.css              # Global styles and TailwindCSS
├── app.html             # HTML template
├── routes/              # SvelteKit routes
│   ├── +layout.svelte   # Main layout component
│   ├── +page.svelte     # Homepage
│   ├── about/           # About page
│   ├── portfolio/       # Portfolio page
│   └── contact/         # Contact page
└── lib/                 # Shared utilities
```

## 🎯 Customization

### Content
- Update text content in each `.svelte` file
- Replace placeholder images with actual project images
- Modify contact information and social links

### Styling
- Colors can be adjusted in `tailwind.config.js`
- Component styles are in `src/app.css`
- Individual page styles can be added to respective components

### Animations
- GSAP animations are configured in each component's `onMount` function
- ScrollTrigger settings can be adjusted for different animation behaviors
- Animation timing and easing can be customized

## 📱 Responsive Design

The website is fully responsive with breakpoints:
- **Mobile**: `< 768px`
- **Tablet**: `768px - 1024px`
- **Desktop**: `> 1024px`

## 🚀 Performance Features

- **Lazy Loading**: Images and components load as needed
- **Optimized Animations**: GSAP animations are optimized for performance
- **Smooth Scrolling**: Lenis provides 60fps smooth scrolling
- **Minimal Bundle**: Optimized for fast loading times

## 🔧 Development Scripts

- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run preview` - Preview production build
- `npm run check` - Type checking and linting
- `npm run format` - Format code with Prettier

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📞 Support

For questions or support, please open an issue in the repository or contact the development team.

---

Built with ❤️ using modern web technologies 