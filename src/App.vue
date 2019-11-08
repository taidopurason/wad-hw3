<template>
    <main id="app">
        <Header/>
        <section id="container">
            <section id="main">
                <div class="content">
                    <Profile :user="user"/>
                    <Courses :courses="courses"/>
                </div>
                <div class="controls">
                    <button id="profile-button" class="pill active">Profile</button>
                    <button id="courses-button" class="pill">Courses</button>
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
        data: () => {
            return {
                courses: [new Course("Web Application Development", 3, 100),
                    new Course("Machine Learning", 3, 85),
                    new Course("Operating Systems", 1, 81),
                    new Course("Parallel Computing", 2, 37)],
                user: new User('John', 'Doe', "11/10/1990", "Software Engineering", 2.75)
            }
        },
        methods: {
            calculateGPA: function () {
                let sum = 0;
                for (let i = 0; i < this.courses.length; i++) {
                    sum += this.getGPAPoint(this.courses[i].grade)
                }
                this.user.gpa = sum / this.courses.length
            },
            getGPAPoint: function (grade) {
                if (grade > 90 && grade <= 100) {
                    return 4;
                } else if (grade > 80) {
                    return 3;
                } else if (grade > 70) {
                    return 2;
                } else if (grade > 60) {
                    return 1;
                } else if (grade > 50) {
                    return 0.5
                } else {
                    return 0;
                }
            }
        },
        beforeMount() {
            this.calculateGPA()
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
