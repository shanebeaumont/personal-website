<script lang="ts">
    import '../styles/global.css';
    import { page } from '$app/state';

    let { children } = $props();

    let menuOpen: boolean = $state(false);

    function toggleMenu() {
        menuOpen = !menuOpen;
    }

    function closeMenu() {
        menuOpen = false;
    }
</script>

<head>
    <title>Shane Beaumont</title>
</head>

<header>
    <button
        id="menu-toggle"
        aria-label={menuOpen ? 'close menu' : 'open menu'}
        onclick={toggleMenu}
    >
        <div class="menu-line"></div>
        <div class="menu-line"></div>
        <div class="menu-line"></div>
    </button>

    <nav class:menu-open={menuOpen}>
        <a
            href="/about"
            class:active={page.url.pathname === "/about"}
            onclick={closeMenu}
        >
            About Me
        </a>

        <a
            href="/blog"
            class:active={page.url.pathname === "/blog"}
            onclick={closeMenu}
        >
            Blog
        </a>

        <a
            href="/"
            class:active={page.url.pathname === "/"}
            onclick={closeMenu}
        >
            Home
        </a>

        <a
            href="/projects"
            class:active={page.url.pathname === "/projects"}
            onclick={closeMenu}
        >
            Projects
        </a>

        <a
            href="/workflow"
            class:active={page.url.pathname === "/workflow"}
            onclick={closeMenu}
        >
            My Workflow
        </a>
    </nav>
</header>

{@render children?.()}

<style>
    header {
        position: sticky;
        top: 0;
        padding: 4px;
        text-align: center;
    }

    nav {
        display: inline-block;
        border-radius: 21px;
        background-color: var(--background-dark);
        transition: right 0.25s ease-out;
    }

    a {
        display: inline-block;
        width: 109px;
        margin: 4px;
        border-radius: 17px;
        padding: 4px 8px;
        font-size: 18px;
        font-weight: bold;
        text-decoration: none;
        color: var(--blue);

        &:hover {
            background-image: linear-gradient(135deg, var(--purple), var(--blue));
            color: var(--background-dark);
            animation: gradient-scroll 0.67s ease-out;
        }

        &:active {
            transform: translateY(2px);
        }
    }

    .active {
        background-image: linear-gradient(135deg, var(--purple), var(--blue));
        color: var(--background-dark);

        &:hover {
            animation: none;
        }
    }

    #menu-toggle {
        display: none;
        position: fixed;
        right: 4px;
        bottom: 4px;
        border: none;
        border-radius: 20.5px;
        padding: 14px 10px 10px 10px;
        background-color: var(--background);
    }

    .menu-line {
        width: 22px;
        height: 2px;
        margin-bottom: 4px;
        border-radius: 1px;
        background-color: var(--foreground);
        pointer-events: none;
    }

    .menu-open {
        right: 0;
    }

    @media (max-width: 688px) {
        a {
            width: 94px;
            font-size: 16px;
        }
    }

    @media (max-width: 613px) {
        header {
            padding: 0;
        }

        nav {
            position: fixed;
            right: -190px;
            bottom: 4px;
            width: 130px;
        }

        a {
            width: 106px;
            font-size: 18px;
        }

        #menu-toggle {
            display: inline-block;
        }
    }

    @keyframes gradient-scroll {
        0% {
            background: linear-gradient(135deg, var(--background-dark), var(--background-dark), #C6A0F6, #8AADF4, #C6A0F6, #8AADF4);
            background-size: 600% 100%;
            background-position: 0% 50%;
            color: var(--blue);
        }

        50% {
            color: var(--background-dark);
        }

        100% {
            background: linear-gradient(135deg, var(--background-dark), var(--background-dark), #C6A0F6, #8AADF4, #C6A0F6, #8AADF4);
            background-size: 600% 100%;
            background-position: 100% 50%;
        }
    }
</style>
