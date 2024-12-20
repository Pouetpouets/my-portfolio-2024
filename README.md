# My Portfolio 2024

A modern, interactive portfolio website built with Svelte, Three.js, and Vite. Features a 3D animated background, smooth transitions, and responsive design.

## Features

- 3D animated background using Three.js
- Responsive navigation with smooth scrolling
- Project showcase with animated cards
- Fun facts section with interactive elements
- Modern, clean UI with animations and transitions
- Fully responsive design

## Tech Stack

- [Svelte](https://svelte.dev/) - Frontend framework
- [TypeScript](https://www.typescriptlang.org/) - Type safety
- [Three.js](https://threejs.org/) - 3D graphics
- [Vite](https://vitejs.dev/) - Build tool

## Getting Started

1. Clone the repository:
```bash
git clone https://github.com/Pouetpouets/my-portfolio-2024.git
cd my-portfolio-2024
```

2. Install dependencies:
```bash
npm install
```

3. Start the development server:
```bash
npm run dev
```

4. Build for production:
```bash
npm run build
```

## Project Structure

- `src/lib/` - Reusable components
  - `ThreeScene.svelte` - 3D background animation
  - `Navigation.svelte` - Main navigation bar
  - `Projects.svelte` - Projects showcase section
  - `FunFacts.svelte` - Fun facts section
- `src/App.svelte` - Main application component
- `src/main.ts` - Application entry point

## Customization

- Update projects in `src/lib/Projects.svelte`
- Modify fun facts in `src/lib/FunFacts.svelte`
- Customize colors and styling in individual component files
- Adjust 3D scene in `src/lib/ThreeScene.svelte`

## License

MIT