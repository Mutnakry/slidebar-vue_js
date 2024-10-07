<template>
  <div>
    <!-- Navbar with button to toggle sidebar -->
    <nav
      class="fixed top-0 z-50 w-full bg-slate-200 border-b border-gray-200 dark:bg-gray-800 dark:border-gray-700"
    >
      <div class="px-3 py-3 lg:px-5 lg:pl-3 flex justify-between">
        <div class="flex items-center">
          <span
            class="text-2xl font-medium"
            :class="sidebarOpen ? 'ms-3' : 'hidden'"
            >ShoppingPOS</span
          >
          <div class="flex items-center justify-start rtl:justify-end">
            <button
              @click="toggleSidebar"
              aria-controls="logo-sidebar"
              type="button"
              class="inline-flex items-center md:ml-20 ml-2 p-2 text-sm text-gray-500 rounded-lg hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-gray-200 dark:text-gray-400 dark:hover:bg-gray-700 dark:focus:ring-gray-600"
            >
              <span class="sr-only">Toggle sidebar</span>
              <svg
                class="w-6 h-6"
                aria-hidden="true"
                fill="currentColor"
                viewBox="0 0 20 20"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  clip-rule="evenodd"
                  fill-rule="evenodd"
                  d="M2 4.75A.75.75 0 012.75 4h14.5a.75.75 0 010 1.5H2.75A.75.75 0 012 4.75zm0 10.5a.75.75 0 01.75-.75h7.5a.75.75 0 010 1.5h-7.5a.75.75 0 01-.75-.75zM2 10a.75.75 0 01.75-.75h14.5a.75.75 0 010 1.5H2.75A.75.75 0 012 10z"
                ></path>
              </svg>
            </button>
          </div>
        </div>

        <div class="flex items-center space-x-4 text-dark">
          <button
            class="bg-green-500 hover:bg-green-600 text-white p-2 rounded"
          >
            <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24">
              <path
                d="M12 0C5.372 0 0 5.373 0 12c0 6.628 5.372 12 12 12s12-5.372 12-12c0-6.628-5.372-12-12-12zm0 20.625c-4.742 0-8.625-3.883-8.625-8.625S7.258 3.375 12 3.375 20.625 7.258 20.625 12 16.742 20.625 12 20.625z"
              />
              <path d="M13.5 11.625h-3V7.5h3v4.125z" />
            </svg>
          </button>
          <button
            class="bg-green-500 space-x-2 flex hover:bg-green-600 text-white p-2 rounded"
          >
           <img class="h-6 w-6" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAwCAYAAABXAvmHAAAACXBIWXMAAAsTAAALEwEAmpwYAAAFeUlEQVR4nO3XW0wUVxgHcOpzdQaRekmsaVO1VlsTmz60TZpITR9qn3zQh/alsTGBGRa1UAqIbKuJN1qk4aKWSC9CLG0FCUGNVkCLCiVqjLUNiJeZYQfYddmlLrDsnPk3MzDjDOyyF9kpSTnJ93Lm7Mz3m3O+c2YTEmbbbJttkTckPJMopL9FPbS9noCCOUpXYvc2iubZXJpnj1M8m6INnStkrKQ5tkiJubxtudZPCewGZSzNMznzO9Pnjd23YA7Np742j0t9IyGejeLZL2iehRIUx16hOOZjimN4rW88jlM8k03x7LA+lmeGKI7Nojjme+NYimMeKvegOfaaoT83bgCaY50Tkp3+4Ni++AFCPHSZIwvvOA9M6l/dl49Vvbsm9a9z7cHinp2hEKOWAFKchXjBkY1N7jJUkXb8ipvI9dVibZ8dL4k5+Mh7HMfkKygll7HZexQvitkqaOvQCeyRz+EzqQ5vu/djiWMn1jjt1gOa0IkL+BtncQcNuI3TuKUiauTrqJY78KPcjkq5DRXyVRyRW1EiX8JhuRmF8m/YJ59XEQVyI/LkBmSROusBLbgbE2Jv4BzsgUYTIofUWw/4Hd1RIxjfSSwQbGrsGPlZR+STBusBV3E/KkSGrwbz+XT991sGv9WXk52csR7QjgcRIzJ9vyDJkPxyMQ8HpQt6Tewl56wHdIAzIZrRBcZbhU3uUlRL7Tri86FaU/IrxTwUBS6aCvsAOT/9gGd7ti2geLZMPWk5Vpq4X9+AYEKUj7To11aIOTghtSF/6LQp+ZfFXSgLtEwq7K/IxaAA5ZOF4pjMRCF1aVTJU3z6eppneqc6MW+hx4Q4FbiBZGG7fl05I4zJrxJ3oSLQGnR3KibN+rgkwaYWdp7UQJIFGxnvdxu/s8K++XDJK/EnxEmIkuGLJoQWr4j5+EG6FnJ3KiWXTQClsAtIIxb27DDex0070paFf/scW66/NUceTo1cx3248ACPTEn9hd6IEKvF3fhJ6phyiz0mXzEBtN0p3V+DpY4s/RrFs99EAuC0H9SN3EQPPBAwAA5uE6AT/VMgmrDCkYs3+/ehVroR0Tmxtm/sc2Jd/5emE3vbcLXxuV1hAcaCdcADEV4dYQTchXNKRLTnxFHSipzh0yghl0yfHaYtlmMC4QGGJJ34B30Y1BHGa/fgmnZEZYhvJ+NzowI8wmMVsdVdaTpF4x2JfDo2uL/WETEDBuDDA+KyLHF6QhyWmlREzAAPhlTEJ+7vLJ+B99xF+nKKGeDFsI7QlpOxJrTdSdli41kTdKyAQYzMCAQdK+AxRlREN3Fis6sci4SQ/2MjipT+Q2iV7+mIVO8J9b+BccxCYTtSXIWokJ58dsQM8MGvIra4jkzb+q7yt+kz8XxPZshx77oK9ZmIGTCEURWx+CnfvJ5UfyHaZU5fTqy3etIMGGdCW04xA4YRUBFWFjZteJZWE9ECRpWByUIG/JBUhJWFTRuepRV2VADliy+RY+XMgRqMQlIRwQo7Xgja8Cxtd4oKoLQAiD0AAiUURLDCjheCNjxL22JjAkjjACWmq4ijiYXCdv2ciBpAVIAMDfGh65jlgI2u4qCFHTZ56n4Gfch75qSb+KAhHMSjIpZYMBOLhB34wFWMs+RO0MIOC6B59g9l4Pq+gyAq4MlMaDWh7U7aOWFlYSdEANAHK4CZgKCfFmD31GMBH/zEVPrzPXUq4nZAwKvi7pDLY42Yj6uBbhXxqacm5D2TeBvSPFU6IkoA49cGe4hPBTwnZEy5bpXrykzsH2wMu8btg/XqTCgHJT3FuGTBps5EC+ky9DP+iGtghkZ7WEAin/b+DEgUwULJLSxgDMFupHmmzbic/rtg/EouESc/22bb/6z9C98FBEpGhnBoAAAAAElFTkSuQmCC">
            <span>POS</span>
          </button>
          <button
            class="bg-green-500 hover:bg-green-600 text-white p-2 rounded"
          >
            <img class="h-6 w-6" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAAACXBIWXMAAAsTAAALEwEAmpwYAAAEWElEQVR4nO2YaYhVZRjHf5rZxIw518pqIgw0mywylYIgm4pCAimJRFrERstogfxi6oekhSgKgpo2XCBbyIialEDMNFvELRL9kNlKCdGqjTNuWZ144v/Gw+HcM/fOPeM5I/OHF+657/Muz/48L/SjH30GJaAVeAf4AujSsN/tmjOawuJEYAHwBxB1M/YC84E6CoYmYKu76GrgduBcoF6jWf+95+i2aG0h0AT8oIuZ+VxWwZqJoo20tqkI5rRVF/oAaKxirdGu19rNeZvZAl1kZwoTF4kmCeb0uzQ/j5xQco5dzpxGOI2VQ4sLACVyQKtz7KS5z4G/nGOnYY1oZpAD2nX4rIS5q4HHNT6pgJE7RPMWOSDYtoXYNDxYASPNLuoddXTq8IYMGGkQTSd9nJGTRNNBDjhmTKtdh1vZUSsjs/N09lYdbrVTrYy8n2f4LSmJRaqdesqIT4iN5IT5zrYbe8CICeNLzd9PjqhTKR6pAKymxCgVqWiMl/G7ZCrdocVpohBlfECTpBrqqjWKROcpzzTo92zn2EEThWEioE6l+N4KW13ziRMoMBoVRt9Wn9KpsVP/zcgrOtUB04DXZdcmzX+A33S5l4FbapDu5cBrwPfAHmAjMDlLBkYBT2vzqILxkxiqFGOAj8rsdUD+tArYr+9XgdOqYeAqYAXwt9vYpHSn6ior8EL4bJaphDAaqQcZ0I2GHwEOOwFYrhkvx9+eIqw3gQu13iykTd//Y5Ck6Tc5CCyJE3bTHIWOsK0MM9ZwfSUaE9QLzl9M2ivd+R8D12t+lP7zHWcYfwLXIAa+dRM/Ag8Ap1I9bnOaXC/mTgGGA6+4M3YAl7p1NwC/aM5M+WY3Z+uXu7U/A48BN0nQkd4F2OfKjJnAYGrDNPUV4eAj7oxIT6mni3YosCz2sHem22uKTC/SHnP0BBVwsubsEYQrgeuAgWQHu+B9wIdiJMneu1zOMYe+25njMDl3oF0HnB07w2gXuQTc6zAbnwo8AawFvhYTnqkO54uTZd6B2XsS/K1BIdtoDgHnkyPq9Xi31JnVS445C80jE9Zd4XzaBDCJgmBIQg6Zk2DqxvizSsZG91lvaGKLzMFa1bmS0khdshzsYhcAzzkmNgCjy1TL37hwuxA4nl7Axgqzf7nRpeBwXAKzbU4L24Cx9DJG69XxeeWQ72JhNz72S8qL5StxtCgwBC08lIUWLPNPUBJLM5csMETmFrRg1ca4Wje1sDcd2B0zgxcT4noWuFZVcNDCwxkk6P8uutoxYJl/kytBDsuMfCbuKYbFMvynWfnCFPck+qu0MsD5wjJXwFm4fEr1VE9woytDDqhzNFPOBCFJLU8pHq0Hf8NpyBh/tIqXlDPUMQYtWDlzDhmjXo1PJRir/iVyBdzClKBgie4u17B16DuthzmquCTmU78DTwIXy1Ss5ro11vO8C5xFQTFRZpKWAHerkOwTGA88Iw3s0WOFdX33xnqKfvSDAuNf+TG5lQBq6zUAAAAASUVORK5CYII=">
          </button>
          <div id="currentDateTime" class="text-gray-900 ">
            {{ currentDateTime }}
          </div>
           <div class="flex items-center">
          <div class="flex items-center ms-3">
            <div>
              <button type="button" class="flex text-md uppercase py-2 bg-gray-300 font-medium  focus:ring-4 focus:ring-gray-300 dark:focus:ring-gray-600" aria-expanded="false" data-dropdown-toggle="dropdown-user">
                <span class="sr-only">Open user menu</span>
                 <p>Nakry</p>
              </button>
            </div>
            <div class="z-50 hidden my-4 w-44 h-44 text-base list-none bg-white divide-y divide-gray-100 rounded shadow dark:bg-gray-700 dark:divide-gray-600" id="dropdown-user">
              <ul class="py-1" role="none">
                <li>
                  <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100 dark:text-gray-300 dark:hover:bg-gray-600 dark:hover:text-white" role="menuitem">Earnings</a>
                </li>
                <li>
                  <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100 dark:text-gray-300 dark:hover:bg-gray-600 dark:hover:text-white" role="menuitem">Sign out</a>
                </li>
              </ul>
            </div>
          </div>
        </div>
        </div>
      </div>
    </nav>

    <!-- Sidebar -->
    <aside
      :class="sidebarOpen ? 'lg:translate-x-0' : '-translate-x-full lg:w-20'"
      class="fixed top-0 left-0 z-40 w-64 h-screen pt-20 transition-transform bg-white border-r border-gray-200 lg:translate-x-0 dark:bg-gray-800 dark:border-gray-700"
      aria-label="Sidebar"
    >
      <div class="h-full px-3 pb-4 overflow-y-auto bg-white dark:bg-gray-800">
        <ul class="space-y-2 font-medium">
          <!-- Dashboard -->
          <li>
            <a
              href="#"
              class="flex items-center p-2 text-gray-900 rounded-lg dark:text-white hover:bg-gray-100 dark:hover:bg-gray-700 group"
            >
              <svg
                class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white"
                aria-hidden="true"
                xmlns="http://www.w3.org/2000/svg"
                fill="currentColor"
                viewBox="0 0 22 21"
              >
                <path
                  d="M16.975 11H10V4.025a1 1 0 0 0-1.066-.998 8.5 8.5 0 1 0 9.039 9.039.999.999 0 0 0-1-1.066h.002Z"
                />
                <path
                  d="M12.5 0c-.157 0-.311.01-.565.027A1 1 0 0 0 11 1.02V10h8.975a1 1 0 0 0 1-.935c.013-.188.028-.374.028-.565A8.51 8.51 0 0 0 12.5 0Z"
                />
              </svg>
              <!-- Conditionally hide/show the title based on sidebar state -->
              <span :class="sidebarOpen ? 'ms-3' : 'hidden'">Dashboard</span>
            </a>
          </li>

          <!-- Kanban -->
          <li>
            <a
              href="#"
              class="flex items-center p-2 text-gray-900 rounded-lg dark:text-white hover:bg-gray-100 dark:hover:bg-gray-700 group"
            >
              <svg
                class="flex-shrink-0 w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white"
                aria-hidden="true"
                xmlns="http://www.w3.org/2000/svg"
                fill="currentColor"
                viewBox="0 0 18 18"
              >
                <path
                  d="M6.143 0H1.857A1.857 1.857 0 0 0 0 1.857v4.286C0 7.169.831 8 1.857 8h4.286A1.857 1.857 0 0 0 8 6.143V1.857A1.857 1.857 0 0 0 6.143 0Zm10 0h-4.286A1.857 1.857 0 0 0 10 1.857v4.286C10 7.169 10.831 8 11.857 8h4.286A1.857 1.857 0 0 0 18 6.143V1.857A1.857 1.857 0 0 0 16.143 0Zm-10 10H1.857A1.857 1.857 0 0 0 0 11.857v4.286C0 17.169.831 18 1.857 18h4.286A1.857 1.857 0 0 0 8 16.143v-4.286A1.857 1.857 0 0 0 6.143 10Zm10 0h-4.286A1.857 1.857 0 0 0 10 11.857v4.286c0 1.026.831 1.857 1.857 1.857h4.286A1.857 1.857 0 0 0 18 16.143v-4.286A1.857 1.857 0 0 0 16.143 10Z"
                />
              </svg>
              <span :class="sidebarOpen ? 'ms-3' : 'hidden'">Kanban</span>
            </a>
          </li>
          <!-- Inbox -->
          <li>
            <a
              href="#"
              class="flex items-center p-2 text-gray-900 rounded-lg dark:text-white hover:bg-gray-100 dark:hover:bg-gray-700 group"
            >
              <svg
                class="flex-shrink-0 w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white"
                aria-hidden="true"
                xmlns="http://www.w3.org/2000/svg"
                fill="currentColor"
                viewBox="0 0 20 20"
              >
                <path
                  d="m17.418 3.623-.018-.008a6.713 6.713 0 0 0-2.4-.569V2h1a1 1 0 1 0 0-2h-2a1 1 0 0 0-1 1v2H9.89A6.977 6.977 0 0 1 12 8v5h-2V8A5 5 0 1 0 0 8v6a1 1 0 0 0 1 1h8v4a1 1 0 0 0 1 1h2a1 1 0 0 0 1-1v-4h6a1 1 0 0 0 1-1V8a5 5 0 0 0-2.582-4.377ZM6 12H4a1 1 0 0 1 0-2h2a1 1 0 0 1 0 2Z"
                />
              </svg>
              <span :class="sidebarOpen ? 'ms-3' : 'hidden'">Inbox</span>
            </a>
          </li>

          <li>
            <button
              type="button"
              value="1"
              class="flex items-center w-full p-2 text-base text-gray-900 transition duration-500 rounded-lg group hover:bg-gray-100 dark:text-white dark:hover:bg-gray-700"
              aria-controls="dropdown-example"
              data-collapse-toggle="dropdown-example"
            >
              <svg
                class="flex-shrink-0 w-5 h-5 text-gray-500 transition duration-75 group-hover:text-gray-900 dark:text-gray-400 dark:group-hover:text-white"
                aria-hidden="true"
                xmlns="http://www.w3.org/2000/svg"
                fill="currentColor"
                viewBox="0 0 18 21"
              >
                <path
                  d="M15 12a1 1 0 0 0 .962-.726l2-7A1 1 0 0 0 17 3H3.77L3.175.745A1 1 0 0 0 2.208 0H1a1 1 0 0 0 0 2h.438l.6 2.255v.019l2 7 .746 2.986A3 3 0 1 0 9 17a2.966 2.966 0 0 0-.184-1h2.368c-.118.32-.18.659-.184 1a3 3 0 1 0 3-3H6.78l-.5-2H15Z"
                />
              </svg>
              <span
                class="flex-1 ms-3 text-left rtl:text-right whitespace-nowrap"
                :class="sidebarOpen ? 'ms-3' : 'hidden'"
                >E-commerce</span
              >
              <svg
                class="w-3 h-3"
                aria-hidden="true"
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 10 6"
              >
                <path
                  stroke="currentColor"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="m1 1 4 4 4-4"
                />
              </svg>
            </button>
            <ul
              id="dropdown-example"
              class="hidden duration-500 py-2 bg-slate-100 space-y-2"
            >
              <li>
                <a
                  href="#"
                  class="flex items-center pl-6 p-2 text-gray-900 rounded-lg dark:text-white hover:bg-gray-100 dark:hover:bg-gray-700 group"
                >
                  <svg
                    class="w-3 h-3 text-gray-800 dark:text-white"
                    aria-hidden="true"
                    xmlns="http://www.w3.org/2000/svg"
                    fill="none"
                    viewBox="0 0 14 10"
                  >
                    <path
                      stroke="currentColor"
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M1 5h12m0 0L9 1m4 4L9 9"
                    />
                  </svg>
                  <span :class="sidebarOpen ? 'ms-3' : 'overflow-hidden'"
                    >Inbox</span
                  >
                </a>
              </li>
              <li>
                <a
                  href="#"
                  class="flex items-center duration-500 pl-6 p-2 text-gray-900 rounded-lg dark:text-white hover:bg-gray-100 dark:hover:bg-gray-700 group"
                >
                  <svg
                    class="w-3 h-3 text-gray-800 dark:text-white"
                    aria-hidden="true"
                    xmlns="http://www.w3.org/2000/svg"
                    fill="none"
                    viewBox="0 0 14 10"
                  >
                    <path
                      stroke="currentColor"
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M1 5h12m0 0L9 1m4 4L9 9"
                    />
                  </svg>
                  <span :class="sidebarOpen ? 'ms-3' : 'overflow-hidden'"
                    >Inbox</span
                  >
                </a>
              </li>
            </ul>
          </li>
        </ul>
      </div>
    </aside>
    <!-- Content -->
    <div
      class="p-4 pt-20 md:ml-64 transition-all duration-300 ease-in-out"
      :class="sidebarOpen ? 'lg:ml-64' : 'lg:ml-20 md:ml-0'"
    >
      <div
        class="p-4 border-2 border-gray-200 border-dashed rounded-lg dark:border-gray-700"
      >
        <!-- Replace this div with your actual content -->
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-4">
          <div class="h-40 rounded bg-red-500 dark:bg-gray-800"></div>
          <div class="h-40 rounded bg-gray-50 dark:bg-gray-800"></div>
          <div class="h-40 rounded bg-gray-50 dark:bg-gray-800"></div>
          <div class="h-40 rounded bg-gray-50 dark:bg-gray-800"></div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      sidebarOpen: true,
      screenWidth: window.innerWidth,
      currentDateTime: ""
    };
  },
  methods: {
    toggleSidebar() {
      this.sidebarOpen = !this.sidebarOpen;
    },
    handleResize() {
      this.screenWidth = window.innerWidth;
      // Automatically hide sidebar on small screens
      if (this.screenWidth < 768) {
        this.sidebarOpen = false;
      } else {
        this.sidebarOpen = true; // You can keep it open if needed
      }
    },

    updateDateTime() {
      const now = new Date();
      this.currentDateTime = now.toLocaleString(); // Formats the date and time
    },
  },
  mounted() {
        this.updateDateTime();
         // Update the time every second
    this.interval = setInterval(this.updateDateTime, 1000);
    window.addEventListener("resize", this.handleResize);
  },
  beforeDestroy() {
    window.removeEventListener("resize", this.handleResize);
     clearInterval(this.interval);
  },
};
</script>

<style>
/* Add any additional styles you need */
</style>