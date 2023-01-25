<template>
    <div>
         <div class="home-search-filters">
            <select id="selectCountry">
                <option value="">Select a Country </option>
                <option value="au">Australia </option>
                <option value="hk">Hong Kong </option>
                <option value="ph">Philippines </option>
                <option value="sk">South Korea </option>
                <option value="us">United States of the America </option>
            </select>
            <select id="selectCategory">
                <option value="">Select a Category </option>
                <option value="business">Business </option>
                <option value="entertainment">Entertainment </option>
                <option value="general">General </option>
                <option value="health">Health </option>
                <option value="science">Science </option>
                <option value="sports">Sports </option>
                <option value="technology">Technology </option>
            </select>
            <input type="text" placeholder="Search" id="inputsearch">
            <button @click="searchNews" id="btnSearchNews">Search</button>
            <button @click="clearAllFilters" id="btnSearchClear">Clear</button>
        </div>

        <div v-if="news && news.length" class="data-table-container">
            <div class="data-table-totalresults">
                <p>{{totalResult}} News Result(s)</p>
            </div>
            <div v-for="post of news" :key="post.id" class="individual-news">
                <div class="news-image-container">
                    <img alt="news logo" :src="post.urlToImage" />
                </div>
                <div class="news-details-container">
                    <p @click="viewNewsDetail(post.id)">{{post.title}}</p>
                    <p>{{post.author}}</p>
                    <p>{{post.description}}</p>
                    <a :href="post.url" target="_blank"><button>Go To Page</button></a>
                </div>
                <div class="news-detail-publisheddate">
                    <p>Published at: {{moment(post.publishedAt).format('YYYY-MM-DD hh:mm')}}</p>
                </div>
            </div>
        </div>
        <div v-else class="data-table-totalresults">
            <p> No results found. </p>
        </div>


        <!-- Modal for viewwing news details -->
    </div>
</template>

<script>
import axios from 'axios';

    export default {
        name: "DataTable",
        data() {
            return {
            news: [],
            totalResult: 0,
            errors: []
            }
        },

        // Fetches news when the component is created.
        created() {
            axios.get(`https://newsapi.org/v2/top-headlines?country=us&apiKey=d2e5c70185754ff0aa63e3d65fc5163a`)
            .then(response => {
                this.news = response.data.articles
                this.totalResult = response.data.totalResults
                console.log(response)
            })
            .catch(e => {
                this.errors.push(e)
            })
        },

        methods: {
            clearAllFilters() {
                document.getElementById("inputsearch").value = "";
                document.getElementById("selectCategory").value = "";
                document.getElementById("selectCountry").value = "";
            },
            searchNews() {
                var selectedCountry = document.getElementById("selectCountry").value;
                var selectedCategory = document.getElementById("selectCategory").value;
                var inputKeyword = document.getElementById("inputsearch").value;

                axios.get(`https://newsapi.org/v2/top-headlines?country=${selectedCountry}&category=${selectedCategory}&q=${inputKeyword}&apiKey=d2e5c70185754ff0aa63e3d65fc5163a`)
                .then(response => {
                    this.news = response.data.articles
                    this.totalResult = response.data.totalResults
                    console.log(response)
                })
                .catch(e => {
                    this.errors.push(e)
                })
            },
            viewNewsDetail(id) {
                alert("THIS NEWS ID " + id)
            }
        }
    };
</script>