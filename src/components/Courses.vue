<template>
    <div id="courses-container" class="tab active">
        <h1 class="title">Courses</h1>
        <table id="courses">
            <thead>
            <tr>
                <th>#</th>
                <th>Course Title</th>
                <th>Semester</th>
                <th>Grade</th>
            </tr>
            </thead>
            <tbody v-for="(course, index) in courses" :key="index">
            <tr>
                <td>{{index}}</td>
                <td>{{course.title}}</td>
                <td>{{course.semester}}</td>
                <td>{{course.grade}}</td>
            </tr>
            </tbody>
        </table>
        <br>
        <br>
        <div id="add-course">
            <button @click="addCourse" id="add-course-button" class="blue-button">+</button>
            <span v-if="isActive">
                                <input class="input" type="text" placeholder="Course title" id="title" v-model="title">
                                <input class="input" type="number" min="1" max="8" placeholder="Semester" id="semester" v-model="semester">
                                <input class="input" type="number" min="0" max="100" placeholder="Grade" id="grade" v-model="grade">
                                <button @click="saveCourse(title, semester, grade) + closeAndResetFields()" class="green-button" id="save-course">Save</button>
                                <button @click="closeAndResetFields" class="grey-button" id="cancel-course">Cancel</button>
                            </span>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Courses",
        data: function () {
            return {
                isActive: false
            }
        },
        props: {
            courses: Array,
            saveCourse: Function
        },
        methods: {
            addCourse: function () {
                this.isActive = !this.isActive;
            },
            closeAndResetFields: function () {
                this.isActive = false
                this.title = null;
                this.semester = null;
                this.grade = null;

            }
        }
    }
</script>

<style scoped>
    #add-course {
        display: flex;
    }

    button {
        margin-right: 5px;
    }

    .input {
        border: 1px solid #cccccc;
        padding: 10px 20px;
        min-width: 135px;
        margin-right: 5px;
    }

    table {
        width: 100%;
        border-collapse: collapse;

    }

    table th {
        padding: 8px 12px;
        text-align: left;
        border: 1px solid #cbcbcb;
        background-color: #03A9F4;
        color: #ffffff;
    }

    table td {
        padding: 8px 12px;
        border: 1px solid #cbcbcb;
    }

    .green-button {
        background-color: #69f378;
        color: #ffffff;
        border: none;
        padding: 10px 10px;
    }

    .grey-button {
        background-color: #e1e8e6;
        color: #ffffff;
        border: none;
        padding: 10px 20px;
    }

    .blue-button {
        background-color: #2196F3;
        color: #ffffff;
        border: none;
        padding: 10px 20px;
    }
</style>