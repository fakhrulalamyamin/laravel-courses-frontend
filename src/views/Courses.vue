<template>
  <div class="mt-1 bg-gray">
    <div class="mx-auto container">
      <div class="flex items-baseline justify-between pt-10">
        <h1 class="text-lg font-bold tracking-tight text-gray-900">
          All Courses
        </h1>
        <div class="flex items-center">
          <div class="relative inline-block text-left">
            <select
              name="sort"
              id="cars"
              class="focus-visible:outline-none py-1 px-2 shadow"
              form="carform"
            >
              <option>Sort</option>
              <option value="Recently Added">Recently Added</option>
              <option value="Most Popular">Most Popular</option>
              <option value="Best Rating">Best Rating</option>
              <option value="Recently Updated">Recently Updated</option>
            </select>
          </div>
        </div>
      </div>
      <div class="pt-6 pb-12">
        <div class="flex gap-x-8 gap-y-10">
          <!-- Filters -->
          <form
            class="w-3/12 block bg-white p-4 px-6 shadow rounded-sm"
            method="GET"
          >
            <h3 class="sr-only">Filters</h3>
            <!--Search-->
            <div class="border-b border-gray-200 py-6">
              <h3 class="-my-3 flow-root">
                <!-- Expand/collapse section button -->
                <button
                  class="flex w-full items-center justify-between bg-white py-3 text-sm text-gray-400 hover:text-gray-500"
                  aria-controls="filter-section-0"
                  aria-expanded="false"
                >
                  <span class="font-medium text-gray-900">Search</span>
                  <span class="ml-6 flex items-center">
                    <svg
                      class="h-5 w-5"
                      xmlns="http://www.w3.org/2000/svg"
                      viewBox="0 0 20 20"
                      fill="currentColor"
                      aria-hidden="true"
                    >
                      <path
                        fill-rule="evenodd"
                        d="M3 10a.75.75 0 01.75-.75h10.5a.75.75 0 010 1.5H3.75A.75.75 0 013 10z"
                        clip-rule="evenodd"
                      ></path>
                    </svg>
                    <svg
                      class="h-5 w-5 hidden"
                      xmlns="http://www.w3.org/2000/svg"
                      viewBox="0 0 20 20"
                      fill="currentColor"
                      aria-hidden="true"
                    >
                      <path
                        d="M10.75 4.75a.75.75 0 00-1.5 0v4.5h-4.5a.75.75 0 000 1.5h4.5v4.5a.75.75 0 001.5 0v-4.5h4.5a.75.75 0 000-1.5h-4.5v-4.5z"
                      ></path>
                    </svg>
                  </span>
                </button>
              </h3>
              <!-- Filter section, show/hide based on section state. -->
              <div class="pt-6">
                <div class="space-y-2">
                  <div class="relative mt-1 rounded-md shadow-sm">
                    <div
                      class="pointer-events-none absolute inset-y-0 left-0 flex items-center pl-3"
                    >
                      <svg
                        class="h-5 w-5 text-gray-400"
                        xmlns="http://www.w3.org/2000/svg"
                        viewBox="0 0 20 20"
                        fill="currentColor"
                        aria-hidden="true"
                      >
                        <path
                          fill-rule="evenodd"
                          d="M9 3.5a5.5 5.5 0 100 11 5.5 5.5 0 000-11zM2 9a7 7 0 1112.452 4.391l3.328 3.329a.75.75 0 11-1.06 1.06l-3.329-3.328A7 7 0 012 9z"
                          clip-rule="evenodd"
                        ></path>
                      </svg>
                    </div>
                    <input
                      type="text"
                      @change="getCourses"
                      v-model="search"
                      class="block w-full rounded border border-gray-300 bg-white py-2 pl-10 pr-3 leading-5 placeholder-gray-500 focus:border-indigo-500 focus:placeholder-gray-400 focus:outline-none focus:ring-1 focus:ring-indigo-500 sm:text-sm"
                      placeholder="Enter keywords"
                    />
                  </div>
                </div>
              </div>
            </div>

            <!--Check Box-->
            <div class="border-b border-gray-200 py-6">
              <h3 class="-my-3 flow-root">
                <!-- Expand/collapse section button -->
                <button
                  type="button"
                  class="flex w-full items-center justify-between bg-white py-3 text-sm text-gray-400 hover:text-gray-500"
                  aria-controls="filter-section-0"
                  aria-expanded="false"
                >
                  <span class="text-gray-900 font-bold">Price</span>
                  <span class="ml-6 flex items-center">
                    <svg
                      class="h-5 w-5"
                      xmlns="http://www.w3.org/2000/svg"
                      viewBox="0 0 20 20"
                      fill="currentColor"
                      aria-hidden="true"
                      x-show="open"
                    >
                      <path
                        fill-rule="evenodd"
                        d="M3 10a.75.75 0 01.75-.75h10.5a.75.75 0 010 1.5H3.75A.75.75 0 013 10z"
                        clip-rule="evenodd"
                      ></path>
                    </svg>
                    <svg
                      class="h-5 w-5"
                      xmlns="http://www.w3.org/2000/svg"
                      viewBox="0 0 20 20"
                      fill="currentColor"
                      aria-hidden="true"
                      x-show="! open"
                      style="display: none"
                    >
                      <path
                        d="M10.75 4.75a.75.75 0 00-1.5 0v4.5h-4.5a.75.75 0 000 1.5h4.5v4.5a.75.75 0 001.5 0v-4.5h4.5a.75.75 0 000-1.5h-4.5v-4.5z"
                      ></path>
                    </svg>
                  </span>
                </button>
              </h3>
              <!-- Filter section, show/hide based on section state. -->
              <div class="pt-6">
                <div class="space-y-2">
                  <div class="flex items-center">
                    <input
                      v-model="price"
                      @change="getCourses"
                      id="filter-price-free"
                      value="free"
                      type="radio"
                      name="price"
                      class="h-4 w-4 rounded border-gray-300 text-indigo-600 focus:ring-indigo-500"
                    />
                    <label
                      for="filter-price-free"
                      class="ml-3 text-sm text-gray-600"
                    >
                      Free <span class="text-xs text-gray-500">(5)</span>
                    </label>
                  </div>
                  <div class="flex items-center">
                    <input
                      v-model="price"
                      @change="getCourses"
                      id="filter-price-onetime"
                      value="paid"
                      type="radio"
                      name="price"
                      class="h-4 w-4 rounded border-gray-300 text-indigo-600 focus:ring-indigo-500"
                    />
                    <label
                      for="filter-price-onetime"
                      class="ml-3 text-sm text-gray-600"
                    >
                      Paid
                      <span class="text-xs text-gray-500">(9)</span>
                    </label>
                  </div>
                </div>
              </div>
            </div>

            <div class="border-b border-gray-200 py-6">
              <h3 class="-my-3 flow-root">
                <!-- Expand/collapse section button -->
                <button
                  type="button"
                  class="flex w-full items-center justify-between bg-white py-3 text-sm text-gray-400 hover:text-gray-500"
                  aria-controls="filter-section-0"
                  aria-expanded="false"
                >
                  <span class="text-gray-900 font-bold">Duration</span>
                  <span class="ml-6 flex items-center">
                    <svg
                      class="h-5 w-5"
                      xmlns="http://www.w3.org/2000/svg"
                      viewBox="0 0 20 20"
                      fill="currentColor"
                      aria-hidden="true"
                      x-show="open"
                    >
                      <path
                        fill-rule="evenodd"
                        d="M3 10a.75.75 0 01.75-.75h10.5a.75.75 0 010 1.5H3.75A.75.75 0 013 10z"
                        clip-rule="evenodd"
                      ></path>
                    </svg>
                    <svg
                      class="h-5 w-5"
                      xmlns="http://www.w3.org/2000/svg"
                      viewBox="0 0 20 20"
                      fill="currentColor"
                      aria-hidden="true"
                      x-show="! open"
                      style="display: none"
                    >
                      <path
                        d="M10.75 4.75a.75.75 0 00-1.5 0v4.5h-4.5a.75.75 0 000 1.5h4.5v4.5a.75.75 0 001.5 0v-4.5h4.5a.75.75 0 000-1.5h-4.5v-4.5z"
                      ></path>
                    </svg>
                  </span>
                </button>
              </h3>
              <!-- Filter section, show/hide based on section state. -->
              <div class="pt-6">
                <div class="space-y-2">
                  <div class="flex items-center">
                    <input
                      v-model="duration"
                      @change="getCourses"
                      id="filter-duration-1h-5h"
                      value="0"
                      type="checkbox"
                      class="h-4 w-4 rounded border-gray-300 text-indigo-600 focus:ring-indigo-500"
                    />
                    <label
                      for="filter-duration-1h-5h"
                      class="ml-3 text-sm text-gray-600"
                    >
                      1-5 hours <span class="text-xs text-gray-500">(16)</span>
                    </label>
                  </div>
                  <div class="flex items-center">
                    <input
                      v-model="duration"
                      @change="getCourses"
                      id="filter-duration-5h-10h"
                      value="1"
                      type="checkbox"
                      class="h-4 w-4 rounded border-gray-300 text-indigo-600 focus:ring-indigo-500"
                    />
                    <label
                      for="filter-duration-5h-10h"
                      class="ml-3 text-sm text-gray-600"
                    >
                      5-10 hours <span class="text-xs text-gray-500">(6)</span>
                    </label>
                  </div>
                  <div class="flex items-center">
                    <input
                      v-model="duration"
                      @change="getCourses"
                      id="filter-duration-10h+"
                      value="2"
                      type="checkbox"
                      class="h-4 w-4 rounded border-gray-300 text-indigo-600 focus:ring-indigo-500"
                    />
                    <label
                      for="filter-duration-10h+"
                      class="ml-3 text-sm text-gray-600"
                    >
                      10+ hours <span class="text-xs text-gray-500">(0)</span>
                    </label>
                  </div>
                </div>
              </div>
            </div>

            <div class="border-b border-gray-200 py-6">
              <h3 class="-my-3 flow-root">
                <!-- Expand/collapse section button -->
                <button
                  type="button"
                  class="flex w-full items-center justify-between bg-white py-3 text-sm text-gray-400 hover:text-gray-500"
                  aria-controls="filter-section-0"
                  aria-expanded="false"
                >
                  <span class="text-gray-900 font-bold">Platform</span>
                  <span class="ml-6 flex items-center">
                    <svg
                      class="h-5 w-5"
                      xmlns="http://www.w3.org/2000/svg"
                      viewBox="0 0 20 20"
                      fill="currentColor"
                      aria-hidden="true"
                      x-show="open"
                    >
                      <path
                        fill-rule="evenodd"
                        d="M3 10a.75.75 0 01.75-.75h10.5a.75.75 0 010 1.5H3.75A.75.75 0 013 10z"
                        clip-rule="evenodd"
                      ></path>
                    </svg>
                    <svg
                      class="h-5 w-5"
                      xmlns="http://www.w3.org/2000/svg"
                      viewBox="0 0 20 20"
                      fill="currentColor"
                      aria-hidden="true"
                      x-show="! open"
                      style="display: none"
                    >
                      <path
                        d="M10.75 4.75a.75.75 0 00-1.5 0v4.5h-4.5a.75.75 0 000 1.5h4.5v4.5a.75.75 0 001.5 0v-4.5h4.5a.75.75 0 000-1.5h-4.5v-4.5z"
                      ></path>
                    </svg>
                  </span>
                </button>
              </h3>
              <!-- Filter section, show/hide based on section state. -->
              <div class="pt-6">
                <div class="space-y-2">
                  <div v-for="platform in platforms" class="flex items-center">
                    <input
                      v-model="selectedPlatforms"
                      @change="getCourses"
                      :id="'filter-platform-' + platform.id"
                      :value="platform.id"
                      type="checkbox"
                      class="h-4 w-4 rounded border-gray-300 text-indigo-600 focus:ring-indigo-500"
                    />
                    <label
                      :for="'filter-platform-' + platform.id"
                      class="ml-3 text-sm text-gray-600"
                    >
                      {{ platform.name }}
                      <span class="text-xs text-gray-500">(4)</span>
                    </label>
                  </div>
                </div>
              </div>
            </div>

            <div class="border-b border-gray-200 py-6">
              <h3 class="-my-3 flow-root">
                <!-- Expand/collapse section button -->
                <button
                  type="button"
                  class="flex w-full items-center justify-between bg-white py-3 text-sm text-gray-400 hover:text-gray-500"
                  aria-controls="filter-section-0"
                  aria-expanded="false"
                >
                  <span class="text-gray-900 font-bold">Series</span>
                  <span class="ml-6 flex items-center">
                    <svg
                      class="h-5 w-5"
                      xmlns="http://www.w3.org/2000/svg"
                      viewBox="0 0 20 20"
                      fill="currentColor"
                      aria-hidden="true"
                      x-show="open"
                    >
                      <path
                        fill-rule="evenodd"
                        d="M3 10a.75.75 0 01.75-.75h10.5a.75.75 0 010 1.5H3.75A.75.75 0 013 10z"
                        clip-rule="evenodd"
                      ></path>
                    </svg>
                    <svg
                      class="h-5 w-5"
                      xmlns="http://www.w3.org/2000/svg"
                      viewBox="0 0 20 20"
                      fill="currentColor"
                      aria-hidden="true"
                      x-show="! open"
                      style="display: none"
                    >
                      <path
                        d="M10.75 4.75a.75.75 0 00-1.5 0v4.5h-4.5a.75.75 0 000 1.5h4.5v4.5a.75.75 0 001.5 0v-4.5h4.5a.75.75 0 000-1.5h-4.5v-4.5z"
                      ></path>
                    </svg>
                  </span>
                </button>
              </h3>
              <!-- Filter section, show/hide based on section state. -->
              <div class="pt-6">
                <div class="space-y-2">
                  <div v-for="item in series" class="flex items-center">
                    <input
                      v-model="selectedSeries"
                      @change="getCourses"
                      :id="'filter-series-' + item.id"
                      :value="item.id"
                      type="checkbox"
                      class="h-4 w-4 rounded border-gray-300 text-indigo-600 focus:ring-indigo-500"
                    />
                    <label
                      :for="'filter-series-' + item.id"
                      class="ml-3 text-sm text-gray-600"
                    >
                      {{ item.name }}
                      <span class="text-xs text-gray-500">(18)</span>
                    </label>
                  </div>
                </div>
              </div>
            </div>
          </form>

          <!--Courses-->
          <div class="w-9/12">
            <div v-if="loading" class="flex">
              <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="1.5"
                stroke="currentColor"
                class="w-6 h-6 animate-spin"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M10.343 3.94c.09-.542.56-.94 1.11-.94h1.093c.55 0 1.02.398 1.11.94l.149.894c.07.424.384.764.78.93.398.164.855.142 1.205-.108l.737-.527a1.125 1.125 0 011.45.12l.773.774c.39.389.44 1.002.12 1.45l-.527.737c-.25.35-.272.806-.107 1.204.165.397.505.71.93.78l.893.15c.543.09.94.56.94 1.109v1.094c0 .55-.397 1.02-.94 1.11l-.893.149c-.425.07-.765.383-.93.78-.165.398-.143.854.107 1.204l.527.738c.32.447.269 1.06-.12 1.45l-.774.773a1.125 1.125 0 01-1.449.12l-.738-.527c-.35-.25-.806-.272-1.203-.107-.397.165-.71.505-.781.929l-.149.894c-.09.542-.56.94-1.11.94h-1.094c-.55 0-1.019-.398-1.11-.94l-.148-.894c-.071-.424-.384-.764-.781-.93-.398-.164-.854-.142-1.204.108l-.738.527c-.447.32-1.06.269-1.45-.12l-.773-.774a1.125 1.125 0 01-.12-1.45l.527-.737c.25-.35.273-.806.108-1.204-.165-.397-.505-.71-.93-.78l-.894-.15c-.542-.09-.94-.56-.94-1.109v-1.094c0-.55.398-1.02.94-1.11l.894-.149c.424-.07.765-.383.93-.78.165-.398.143-.854-.107-1.204l-.527-.738a1.125 1.125 0 01.12-1.45l.773-.773a1.125 1.125 0 011.45-.12l.737.527c.35.25.807.272 1.204.107.397-.165.71-.505.78-.929l.15-.894z"
                />
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"
                />
              </svg>
              <p class="ml-3">Loading ...</p>
            </div>
            <ul v-else role="list" class="space-y-6">
              <!--Single Course-->
              <CourseBigBox
                v-for="course in courses"
                :key="course.id"
                :course="course"
              />
            </ul>

            <!--Pagination-->
            <div class="mt-5">
              <nav
                role="navigation"
                aria-label="Pagination Navigation"
                class="flex items-center justify-between"
              >
                <div class="flex justify-between flex-1 sm:hidden">
                  <span
                    class="relative inline-flex items-center px-4 py-2 text-sm font-medium text-gray-500 bg-white border border-gray-300 cursor-default leading-5 rounded-md"
                  >
                    « Previous
                  </span>
                  <a
                    href="#"
                    class="relative inline-flex items-center px-4 py-2 ml-3 text-sm font-medium text-gray-700 bg-white border border-gray-300 leading-5 rounded-md hover:text-gray-500 focus:outline-none focus:ring ring-gray-300 focus:border-blue-300 active:bg-gray-100 active:text-gray-700 transition ease-in-out duration-150"
                  >
                    Next »
                  </a>
                </div>
                <div
                  class="hidden sm:flex-1 sm:flex sm:items-center sm:justify-between"
                >
                  <div>
                    <p class="text-sm text-gray-700 leading-5">
                      Showing <span class="font-medium">1</span> to
                      <span class="font-medium">10</span> of
                      <span class="font-medium">24</span> results
                    </p>
                  </div>
                  <div>
                    <span class="relative z-0 inline-flex shadow-sm rounded-md">
                      <span
                        aria-disabled="true"
                        aria-label="&amp;laquo; Previous"
                      >
                        <span
                          class="relative inline-flex items-center px-2 py-2 text-sm font-medium text-gray-500 bg-white border border-gray-300 cursor-default rounded-l-md leading-5"
                          aria-hidden="true"
                        >
                          <svg
                            class="w-5 h-5"
                            fill="currentColor"
                            viewBox="0 0 20 20"
                          >
                            <path
                              fill-rule="evenodd"
                              d="M12.707 5.293a1 1 0 010 1.414L9.414 10l3.293 3.293a1 1 0 01-1.414 1.414l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 0z"
                              clip-rule="evenodd"
                            ></path>
                          </svg>
                        </span>
                      </span>
                      <span aria-current="page">
                        <span
                          class="relative inline-flex items-center px-4 py-2 -ml-px text-sm font-medium text-gray-500 bg-white border border-gray-300 cursor-default leading-5"
                          >1</span
                        >
                      </span>
                      <a
                        href="#"
                        class="relative inline-flex items-center px-4 py-2 -ml-px text-sm font-medium text-gray-700 bg-white border border-gray-300 leading-5 hover:text-gray-500 focus:z-10 focus:outline-none focus:ring ring-gray-300 focus:border-blue-300 active:bg-gray-100 active:text-gray-700 transition ease-in-out duration-150"
                        aria-label="Go to page 2"
                      >
                        2
                      </a>
                      <a
                        href="#"
                        class="relative inline-flex items-center px-4 py-2 -ml-px text-sm font-medium text-gray-700 bg-white border border-gray-300 leading-5 hover:text-gray-500 focus:z-10 focus:outline-none focus:ring ring-gray-300 focus:border-blue-300 active:bg-gray-100 active:text-gray-700 transition ease-in-out duration-150"
                        aria-label="Go to page 3"
                      >
                        3
                      </a>
                      <a
                        href="#"
                        rel="next"
                        class="relative inline-flex items-center px-2 py-2 -ml-px text-sm font-medium text-gray-500 bg-white border border-gray-300 rounded-r-md leading-5 hover:text-gray-400 focus:z-10 focus:outline-none focus:ring ring-gray-300 focus:border-blue-300 active:bg-gray-100 active:text-gray-500 transition ease-in-out duration-150"
                        aria-label="Next &amp;raquo;"
                      >
                        <svg
                          class="w-5 h-5"
                          fill="currentColor"
                          viewBox="0 0 20 20"
                        >
                          <path
                            fill-rule="evenodd"
                            d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z"
                            clip-rule="evenodd"
                          ></path>
                        </svg>
                      </a>
                    </span>
                  </div>
                </div>
              </nav>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import CourseBigBox from "../components/CourseBigBox.vue";

export default {
  name: "CoursesPage",
  data() {
    return {
      search: "",
      courses: [],
      price: "",
      duration: [],
      platforms: [],
      series: [],
      selectedSeries: [],
      selectedPlatforms: [],
      loading: true,
    };
  },
  mounted() {
    this.getCourses();
  },
  methods: {
    getCourses() {
      this.loading = true;
      axios
        .get("https://laravel-courses.test/api/all-courses", {
          params: {
            search: this.search,
            price: this.price,
            duration: this.duration,
            series: this.selectedSeries,
            platform: this.selectedPlatforms,
          },
        })
        .then((response) => {
          this.courses = response.data.courses;
          this.series = response.data.series;
          this.platforms = response.data.platforms;

          this.loading = false;
        });
    },
  },
  components: { CourseBigBox },
};
</script>
