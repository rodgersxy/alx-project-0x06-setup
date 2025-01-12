# Reactify TS: Mastering Advanced TypeScript in React    

Tasks
0. Implementing a share layout
mandatory
Objective: In most applications, you will have multiple pages that share similar Layout (i.e. Header and Footer). This can be achieved in multiple ways. You have already seen how you can do this by reusing your Header and Footer Components on Multiple pages. But there is a better way to do this and that is through the DRY framework. Set up a base application using create-next-app@latest with the name alx-project-0x03 in a Github repository alx-project-0x03-setup .

Instructions:

Install the following third party dependency react-icons/fa
Create the following Components under the components/layouts
components/layouts/Header.tsx
components/layouts/Footer.tsx
components/layouts/Layout.tsx
components/common/Button.tsx
Replace the content of each file with the code below
## components/common/Button.tsx

interface ButtonProps {
  buttonLabel: string
  buttonSize?: string
  buttonBackgroundColor?: 'red' | 'blue' | 'orange' | 'green'
  action?: () => void
}


const Button = ({ buttonLabel, buttonSize, buttonBackgroundColor, action }: ButtonProps) => {

  const backgroundColorClass = buttonBackgroundColor ? {
    red: 'bg-red-500',
    blue: 'bg-blue-500',
    orange: 'bg-orange-500',
    green: 'bg-green-500',
  }[buttonBackgroundColor] : 'bg-slate-500'


  return (
    <button onClick={action} className={`${backgroundColorClass} ${buttonSize} px-6 py-2 text-sm font-semibold rounded-lg hover:${backgroundColorClass}/50 transition duration-300 text-white`}>
      {buttonLabel}
    </button>
  )
}

export default Button;

### components/layouts/Header.tsx

import Link from "next/link";
import Button from "../common/Button";

const Header: React.FC = () => {
  return (
    <header className="fixed w-full bg-white shadow-md">
      <div className="container mx-auto flex justify-between items-center py-6 px-4 md:px-8">
        <Link href="/" className="text-3xl md:text-5xl font-bold text-gray-800 tracking-tight">
          Splash App
        </Link>

        {/* Button Group */}
        <div className="flex gap-4">
          <Button
            buttonLabel="Sign In"
            buttonBackgroundColor="red"
          />
          <Button
            buttonLabel="Sign Up"
            buttonBackgroundColor="blue"
          />
        </div>
      </div>
    </header>
  );
};

export default Header;
## components/layouts/Footer.tsx

import { 
FaFacebook, 
FaTwitter,
FaInstagram } from 'react-icons/fa'; 

const Footer: React.FC = () => {
  return (
    <footer className="bg-gray-900 text-white py-10">
      <div className="container mx-auto grid grid-cols-1 md:grid-cols-3 gap-8">
        <div>
          <h3 className="text-xl font-bold mb-4">Splash App</h3>
          <p className="text-gray-400 mb-4">
            Your one-stop platform for all your needs. Connecting people, creating opportunities.
          </p>
          <p className="text-gray-400">© 2024 Splash App. All rights reserved.</p>
        </div>

        <div>
          <h4 className="text-lg font-semibold mb-4">Useful Links</h4>
          <ul>
            <li className="mb-2">
              <a href="/about" className="text-gray-400 hover:text-white transition duration-300">
                About Us
              </a>
            </li>
            <li className="mb-2">
              <a href="/services" className="text-gray-400 hover:text-white transition duration-300">
                Services
              </a>
            </li>
            <li className="mb-2">
              <a href="/contact" className="text-gray-400 hover:text-white transition duration-300">
                Contact Us
              </a>
            </li>
          </ul>
        </div>

        <div>
          <h4 className="text-lg font-semibold mb-4">Follow Us</h4>
          <div className="flex space-x-4">
            <a href="https://facebook.com" target="_blank" rel="noopener noreferrer" className="text-gray-400 hover:text-white transition duration-300">
              <FaFacebook size={24} />
            </a>
            <a href="https://twitter.com" target="_blank" rel="noopener noreferrer" className="text-gray-400 hover:text-white transition duration-300">
              <FaTwitter size={24} />
            </a>
            <a href="https://instagram.com" target="_blank" rel="noopener noreferrer" className="text-gray-400 hover:text-white transition duration-300">
              <FaInstagram size={24} />
            </a>
          </div>
        </div>
      </div>
    </footer>
  );
}

export default Footer;

import { ReactNode } from "react";
import Footer from "./Footer";
import Header from "./Header";

interface LayoutProps {
  children: ReactNode;
}

const Layout: React.FC<LayoutProps> = ({ children }) => {
  return (
    <>
      <Header />
      <main>{children}</main>
      <Footer />
    </>
  );
};

export default Layout;
Save and close your files
Run npm run dev from the terminal
From a tab in your browser type http://localhost:3000 to see the changes made.
Repo:

GitHub repository: alx-project-0x03-setup
Directory: alx-project-0x03
File: components/common/Button.tsx, components/layouts/Header.tsx, components/layouts/Footer.tsx, components/layouts/Layout.tsx
1. Importing Google fonts
mandatory
Objectives: By default your project will include some tailwindcss configurations. We can import a google font to be included in the global space of our tailwindcss. We will see how to do this in our global.css file.

Instructions:

We are going to use the Montserrate fonts from google fonts. Note that you can explore other fonts directly from google fonts page.
Open the file styles/global.css.
Replace the content with the following
@import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap');

@tailwind base;
@tailwind components;
@tailwind utilities;

body {
  font-family: "Montserrat", sans-serif;
  font-optical-sizing: auto;
}
Note, that this will apply the Montserrat fonts to every element on a page rendered.
Open the file pages/index.tsx
Replace the content with the following.
const Home = () => {
  return (
   <div>
    <h1> Welcome to Splash App </h1>
   </div>
}

export default Home;
Save and close your files
Run npm run dev from the terminal
From a tab in your browser type http://localhost:3000 to see the changes m
Repo:

GitHub repository: alx-project-0x03-setup
Directory: alx-project-0x03
File: pages/index.tsx, styles/global.css
2. Setting up our landing page with Imperative routing
mandatory
Objectives: Our App will have 3 additional mini apps. This can be accessible through imperative routing. Which means we need to use the Link component explicitly but by using useRouter Hook from next/router.

We will modify our index.tsx file to achieve this functionality
Instructions:

Open pages/index.tsx file and replace the content with the code below.
import Button from "@/components/common/Button";
import { useRouter } from "next/router";

interface PageRouteProps {
  pageRoute: string
}

export default function Home() {
  const router = useRouter()

  // Imeperative routing with useRouter
  const routeToNextPage  = ({ pageRoute }: PageRouteProps) => {
    router.push(pageRoute, undefined, { shallow: false})
  }

  return (
    <div className="min-h-screen bg-gray-100 flex flex-col justify-center items-center text-center">
      {/* Welcome Message */}
      <h1 className="text-4xl font-bold text-gray-800 mb-4">
        Welcome to Splash App!
      </h1>
      <p className="text-lg text-gray-600 mb-8">
        Your one-stop platform for everything AI you need. Start exploring by
        navigating to our features below.
      </p>

      {/* Navigation Options */}
      <div className="flex gap-6">
        <Button action={() => routeToNextPage({ pageRoute: '/generate-text-ai' })} buttonLabel="Generate Text" buttonBackgroundColor="blue" />
        <Button action={() => routeToNextPage({ pageRoute: '/text-to-image'})} buttonLabel="Text to Image" buttonBackgroundColor="green" />
        <Button action={() => routeToNextPage({ pageRoute: '/counter-app'})} buttonLabel="Contact us" buttonBackgroundColor="orange" />
      </div>
    </div>
  );
}

Note the use of the Button component.
Each button accepts an action prop, which is a function with an additional argument of pageRoute. The function uses an instance of next/route to implicitly navigate users to the specified path name.
 // Imeperative routing with useRouter
  const routeToNextPage  = ({ pageRoute }: PageRouteProps) => {
    router.push(pageRoute, undefined, { shallow: false})
  }
Save and close your files
Run npm run dev from the terminal
From a tab in your browser type http://localhost:3000 to see the changes made.
Note that when you click on the buttons. It takes you to a 404 page not found. But its still wrapped with our Header and Footer.
Repo:

GitHub repository: alx-project-0x03-setup
Directory: alx-project-0x03
File: pages/index.tsx
3. Move your interfaces to the right directory
mandatory
Objectives: Clean up your code a bit, remember, it is always good to keep your code well organized. Group your files into the right directories.

Instructions:

Create an empty directory interface, under your project root directory.
Create a file index.ts in the interface directory
Extract the interface from the files: pages/index.tsx, components/common/Button.tsx, components/layouts/Layout.tsx and place them in interface/index.ts
Export each interface
At the top of each of these files pages/index.tsx, components/common/Button.tsx, components/layouts/Layout.tsx, import the right interfaces to be used.

Save and close your files

Run npm run dev from the terminal

From a tab in your browser type http://localhost:3000 to see the changes made.

Your pages should work as usual, but you will realize it is easier to manage all your interfaces under a similar file.

Repo:

GitHub repository: alx-project-0x03-setup
Directory: alx-project-0x03
File: interface/index.tsx, pages/index.tsx, components/common/Button.tsx, components/layouts/Layout.tsx
4. Resolve a 404 page not found
mandatory
Objectives: In the file-based routing system, each pathname has to correspond to a particular file that exists in the pages/ directory. In an event where any such pathname is used but not found in the pages directory. Your routing will resolve to a 404 page not found.

This is a default behavior in Nextjs applications. The behavior can be overridden if you wish to have a Custom Error Page

Instructions:

From your pages/ directory create a file 404.tsx
Replace the content of this file with the code below:
import Link from 'next/link';
import { FaHome } from 'react-icons/fa'; 

const Custom404 = () => {
  return (
    <div className="min-h-screen bg-gradient-to-r from-purple-500 to-pink-500 flex flex-col justify-center items-center text-white">
      {/* Main Heading */}
      <h1 className="text-6xl font-bold mb-4">Oops! 😱</h1>
      <p className="text-2xl mb-8">
        We can't seem to find the page you're looking for.
      </p>

      {/* Funny Message */}
      <p className="text-lg mb-8 text-center max-w-md">
        Maybe it was abducted by aliens 👽, or it just took a wrong turn into the Internet wilderness! Either way, it's not here.
      </p>

      {/* Button to navigate back */}
      <Link
        href="/"
        className="flex items-center space-x-2 bg-blue-500 hover:bg-blue-600 text-white font-semibold py-3 px-6 rounded-lg transition duration-300"
      >
        <FaHome size={20} />
        <span>Go Back Home</span>
      </Link>
    </div>
  );
}

export default Custom404;

Save and close your files
Run npm run dev from the terminal
From a tab in your browser type http://localhost:3000/unknown-pathname to see the changes made.
Repo:

GitHub repository: alx-project-0x03-setup
Directory: alx-project-0x03
File: pages/404.tsx
