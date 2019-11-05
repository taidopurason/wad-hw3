<template>
    <footer>
        <ul v-for="(link, index) in links" :key="index" class="links">
            <li>
                <a v-bind:href="link.link" target="_blank">{{link.title}}</a>
            </li>
        </ul>
    </footer>
</template>

<script>
    import Link from '../models/Link'

    export default {
        name: "Footer",
        data: () => {
            return{
                links: [new Link("OIS", "https://ois2.ut.ee/"), new Link("Courses", "https://courses.cs.ut.ee/")]
            }
        }
    }
</script>

<style scoped>
    footer {
        padding: 30px 0;
        background-color: #607D8B;
        margin-top: 10px;
        height: 100px;
        position: absolute;
        bottom: 0;
        width: 100%;
    }

    footer .links {
        display: block;
        width: 100%;
        max-width: 200px;
        margin: 0 auto;
        color: #acd7ff;
        font-size: 11px;
    }

    footer .links a {
        text-decoration: none;
        color: #acd7ff;
    }

    footer .links a:hover {
        text-decoration: underline;
    }
</style>