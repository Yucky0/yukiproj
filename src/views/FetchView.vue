<template>
  <main class="fetch">
    <h2>Courses Available</h2>
    <p>Select a course subject to see the classes and sections available:</p>
    <label>
      Course Subjects:
      <select name="type" id="type" v-model="selectedSubject">
        <option
          v-for="subject in CourseSubjects"
          :key="subject"
          :value="subject"
        >
          {{ subject }}
        </option>
      </select>
    </label>
    <table>
      <thead>
        <tr>
          <th>Class</th>
          <th>Class section available</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(course, index) in courses" :key="index">
          <td>{{ course.class }}</td>
          <td>{{ course.section }}</td>
        </tr>
      </tbody>
    </table>
  </main>
</template>

<script setup>
import { ref, watch } from 'vue';

const CourseSubjects = ['CSE', 'MATH', 'ENGL', 'HIST', 'CHEM', 'OPIM'];
const selectedSubject = ref(CourseSubjects[0]);

// this adds the course data for the classes
const coursesData = {
  CSE: [
    { class: 'CSE1010', section: 'Section 1' },
    { class: 'CSE2050', section: 'Section 2' },
    { class: 'CSE2102', section: 'Section 3' },
  ],
  MATH: [
    { class: 'MATH1030Q', section: 'Section 1' },
    { class: 'MATH1060Q', section: 'Section 2' },
    { class: 'MATH1151Q', section: 'Section 3' },
  ],
  ENGL: [
    { class: 'ENGL2100', section: 'Section 1' },
    { class: 'ENGL2201', section: 'Section 2' },
    { class: 'ENGL3303', section: 'Section 3' },
  ],
  HIST: [
    { class: 'HIST2020', section: 'Section 1' },
    { class: 'HIST2470', section: 'Section 2' },
    { class: 'HIST3400', section: 'Section 3' },
  ],
  CHEM: [
    { class: 'CHEM2443', section: 'Section 1' },
    { class: 'CHEM2444', section: 'Section 2' },
    { class: 'CHEM2445', section: 'Section 3' },
  ],
  OPIM: [
    { class: 'OPIM3103', section: 'Section 1' },
    { class: 'OPIM3104', section: 'Section 2' },
    { class: 'OPIM3401', section: 'Section 3' },
  ],
};

const courses = ref(coursesData[selectedSubject.value] || []);

// Watches the changes when user selects a different course subject and adjusts the table accordingly
watch(selectedSubject, () => {
  courses.value = coursesData[selectedSubject.value] || [];
});
</script>

<style>
/* add padding around the page */
.fetch {
  padding: 1rem;
}

/* make the heading font larger and add spacing below */
.fetch h2 {
  font-size: 1.5rem;
  margin-bottom: 2rem;
}

/* add spacing below the text */
.fetch p {
  margin-bottom: 1rem;
}

/* add borders to the table and its top row */
.fetch table,
.fetch thead {
  border: 1px solid #d9d9d9;
}

/* setup the spacing and the text alignment of the table headers and table cells */
.fetch :is(th, td) {
  text-align: left;
  padding: 0.25rem 0.75rem;
  min-width: 10rem;
}

/* make even numbered rows an off-white color to make the table more legible */
.fetch tr:nth-child(even) {
  background-color: #f9f9f9;
}
</style>
