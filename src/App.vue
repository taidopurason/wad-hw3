<template>
    <main id="app">
        <Header/>
        <section id="container">
            <section id="main">
                <div class="content">
                    <Profile v-if="!isActive" :user="user" :courses="courses"/>
                    <Courses v-if="isActive" :courses="courses" :save-course="addCourse"/>
                </div>
                <div class="controls">
                    <button @click="seeProfile" v-bind:class="[isActive ? 'pill' : 'pill active']" id="profile-button" class="pill">Profile</button>
                    <button @click="seeCourses" id="courses-button" v-bind:class="[!isActive ? 'pill' : 'pill active']" class="pill">Courses</button>
                </div>
            </section>
        </section>
        <Footer/>


    </main>
</template>

<script>
    import Profile from "./components/Profile";
    import Courses from "./components/Courses";
    import Footer from "./components/Footer";
    import Course from './models/Course'
    import User from './models/User'
    import Header from "./components/Header";

    export default {
        name: 'app',
        components: {Footer, Courses, Profile, Header},
        props: {

        },
        data: () => {
            return {
                courses: [new Course("Web Application Development", 3, 100),
                    new Course("Machine Learning", 3, 85),
                    new Course("Operating Systems", 1, 81),
                    new Course("Parallel Computing", 2, 37)],
                user: new User('John', 'Doe', "11/10/1990", "Software Engineering", 2.75),
                isActive: false
            }
        },
        methods: {
            addCourse: function (name, semester, grade) {
                this.courses.push(new Course(name, semester, grade));
                // this.calculateGPA()
            },
            seeProfile: function () {
                this.isActive = false
            },
            seeCourses: function () {
                this.isActive = true
            }
        }
    }
</script>

<style>
    * {
        box-sizing: border-box;
        font-family: 'Livvic', sans-serif;
    }

    html, body {
        padding: 0;
        margin: 0;
        width: 100%;
        height: 100%;
        background-color: #eaeaea;
    }

    main {
        position: relative;
        min-height: 100%;
        padding-bottom: 110px;
    }

    .clear-fix {
        clear: both;
    }

    button {
        margin-right: 5px;
    }

    #container {
        width: 80%;
        max-width: 900px;
        min-width: 320px;
        padding: 15px;
        background-color: #ffffff;
        margin: 0 auto;
    }


    .content {
        padding: 10px;
        border: 1px solid #cbcbcb;
    }

    .content .tab {
        display: none;
    }

    .content .tab.active {
        display: block;
    }

    .controls .pill {
        border: 1px solid #cbcbcb;
        background-color: #eaeaea;
        padding: 10px;
        border-bottom-left-radius: 4px;
        border-bottom-right-radius: 4px;
        border-top: none;
        margin-top: -1px;
        outline: none !important;
    }

    .controls .pill.active {
        background-color: #ffffff;
        border-top: 1px solid #ffffff;
    }

    .controls .pill:hover {
        cursor: pointer;
    }
</style>
