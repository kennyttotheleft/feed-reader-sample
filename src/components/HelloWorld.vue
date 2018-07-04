<template>
  <div id="issues">
    <h1>Latest Issues</h1>
    <div>
      Repository: <input type="text" v-model="repository">
    </div>
    <div>
      <input type="text" v-model="searchText">
      <div v-show="hasIssue">
        <div v-for="issue in filtered_issues" :key="issue.id"
            class="issue-default">
          <a :href="issue.html_url" target="_blank">
            {{issue.title}}
          </a><br/>
          <span>#{{issue.number}} at {{issue.updated_at | formatDate}}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// Open issues from vuejs/vuejs.org repository.
const ISSUES = 'https://api.github.com/repos/[R]/issues?state=open'

export default {
  name: 'HelloWorld',
  data () {
    return {
      repository: 'vuejs/vuejs.org',
      searchText: '',
      msg: 'Welcome to Your Vue.js App',
      issues: []
    }
  },
  created: function () {
    this.fetchData()
  },
  watch: {
    repository: 'fetchData'
  },
  filters: {
    formatDate: function (v) {
      return v.replace(/T|Z/g, ' ')
    }
  },
  computed: {
    hasIssue: function () {
      return this.issues.length > 0
    },
    filtered_issues: function () {
      let query = this.searchText
      return this.issues.filter(function (issue) {
        return issue.title.indexOf(query) > -1
      })
    }
  },
  methods: {
    fetchData: function () {
      var xhr = new XMLHttpRequest()
      var self = this
      xhr.open('GET', ISSUES.replace('[R]', self.repository))
      xhr.onload = function () {
        self.issues = JSON.parse(xhr.responseText)
      }
      xhr.send()
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
