<template>
  <v-container>

    <div class="text-center mb-8">

      <h1 class="text-h3 font-weight-bold">
        Data Table Showcase
      </h1>

      <p class="text-subtitle-1 mt-2">
        Reusable Vue 3 + Vuetify Data Table Component
      </p>

    </div>


    <v-card
      class="mb-8"
      elevation="3"
      rounded="lg"
    >

      <BaseDataTable
        title="Inventory Management"
        :columns="inventoryColumns"
        :items="inventory"
      />

    </v-card>



    <v-card
      class="mb-8"
      elevation="3"
      rounded="lg"
    >

      <BaseDataTable
        title="Financial Transactions"
        :columns="transactionColumns"
        :items="transactions"
      />

    </v-card>



    <v-card
      class="mb-8"
      elevation="3"
      rounded="lg"
    >

      <BaseDataTable
        title="Task / Project Management"
        :columns="taskColumns"
        :items="tasks"
      />

    </v-card>



    <v-card
      class="mb-8"
      elevation="3"
      rounded="lg"
    >

      <BaseDataTable
        title="Customer Support Tickets"
        :columns="ticketColumns"
        :items="tickets"
      />

    </v-card>


  </v-container>
</template>

<script setup>

import BaseDataTable from "../components/BaseDataTable.vue"


// ================= INVENTORY MANAGEMENT =================

const inventoryColumns = [
  { title:"Product", key:"product" },
  { title:"Category", key:"category" },
  { title:"Stock", key:"stock" },
  { title:"Price", key:"price" }
]


const inventory = [
  {id:1, product:"Laptop", category:"Electronics", stock:15, price:55000},
  {id:2, product:"Keyboard", category:"Accessories", stock:40, price:1500},
  {id:3, product:"Mouse", category:"Accessories", stock:55, price:800},
  {id:4, product:"Monitor", category:"Electronics", stock:20, price:12000},
  {id:5, product:"Printer", category:"Office", stock:12, price:9000},
  {id:6, product:"Tablet", category:"Electronics", stock:18, price:25000},
  {id:7, product:"Webcam", category:"Accessories", stock:30, price:3000},
  {id:8, product:"Headphones", category:"Audio", stock:45, price:2200},
  {id:9, product:"Speaker", category:"Audio", stock:25, price:4500},
  {id:10, product:"Router", category:"Networking", stock:35, price:3500},
  {id:11, product:"SSD", category:"Storage", stock:22, price:6000},
  {id:12, product:"Hard Drive", category:"Storage", stock:28, price:5000},
  {id:13, product:"USB Cable", category:"Accessories", stock:70, price:400},
  {id:14, product:"Mobile Stand", category:"Accessories", stock:60, price:700},
  {id:15, product:"Smart Watch", category:"Wearable", stock:16, price:8000},
  {id:16, product:"Camera", category:"Electronics", stock:10, price:30000},
  {id:17, product:"Microphone", category:"Audio", stock:14, price:6000},
  {id:18, product:"Power Bank", category:"Accessories", stock:50, price:1800},
  {id:19, product:"Charger", category:"Accessories", stock:65, price:1200},
  {id:20, product:"Projector", category:"Office", stock:8, price:45000}
]


// ================= FINANCIAL TRANSACTIONS =================

const transactionColumns = [
  { title:"Transaction ID", key:"transactionId" },
  { title:"User", key:"user" },
  { title:"Amount", key:"amount" },
  { title:"Status", key:"status" }
]


const transactions = [
  {id:1, transactionId:"TXN001", user:"Rajat", amount:2500, status:"Completed"},
  {id:2, transactionId:"TXN002", user:"Rahul", amount:4200, status:"Pending"},
  {id:3, transactionId:"TXN003", user:"Amit", amount:1800, status:"Completed"},
  {id:4, transactionId:"TXN004", user:"Neha", amount:5600, status:"Failed"},
  {id:5, transactionId:"TXN005", user:"Priya", amount:3200, status:"Completed"},
  {id:6, transactionId:"TXN006", user:"Arjun", amount:7500, status:"Pending"},
  {id:7, transactionId:"TXN007", user:"Karan", amount:2100, status:"Completed"},
  {id:8, transactionId:"TXN008", user:"Riya", amount:8900, status:"Completed"},
  {id:9, transactionId:"TXN009", user:"Simran", amount:1500, status:"Failed"},
  {id:10, transactionId:"TXN010", user:"Ankit", amount:6700, status:"Completed"},
  {id:11, transactionId:"TXN011", user:"Vikas", amount:4300, status:"Pending"},
  {id:12, transactionId:"TXN012", user:"Rohit", amount:2900, status:"Completed"},
  {id:13, transactionId:"TXN013", user:"Sneha", amount:6100, status:"Completed"},
  {id:14, transactionId:"TXN014", user:"Pooja", amount:3800, status:"Failed"},
  {id:15, transactionId:"TXN015", user:"Deepak", amount:9200, status:"Completed"},
  {id:16, transactionId:"TXN016", user:"Mohit", amount:2700, status:"Pending"},
  {id:17, transactionId:"TXN017", user:"Nikita", amount:5400, status:"Completed"},
  {id:18, transactionId:"TXN018", user:"Yash", amount:3300, status:"Completed"},
  {id:19, transactionId:"TXN019", user:"Aditya", amount:4800, status:"Pending"},
  {id:20, transactionId:"TXN020", user:"Ayesha", amount:7100, status:"Completed"}
]
// ================= TASK / PROJECT MANAGEMENT =================

const taskColumns = [
  { title:"Task", key:"task" },
  { title:"Assigned To", key:"assignedTo" },
  { title:"Priority", key:"priority" },
  { title:"Status", key:"status" }
]


const tasks = [
  {id:1, task:"Design Homepage", assignedTo:"Rajat", priority:"High", status:"Completed"},
  {id:2, task:"Create API", assignedTo:"Rahul", priority:"High", status:"In Progress"},
  {id:3, task:"Database Setup", assignedTo:"Amit", priority:"Medium", status:"Completed"},
  {id:4, task:"Testing", assignedTo:"Neha", priority:"Low", status:"Pending"},
  {id:5, task:"UI Improvements", assignedTo:"Priya", priority:"Medium", status:"In Progress"},
  {id:6, task:"Authentication", assignedTo:"Arjun", priority:"High", status:"Completed"},
  {id:7, task:"Bug Fixing", assignedTo:"Karan", priority:"Low", status:"Pending"},
  {id:8, task:"Documentation", assignedTo:"Riya", priority:"Medium", status:"Completed"},
  {id:9, task:"Deployment", assignedTo:"Simran", priority:"High", status:"Pending"},
  {id:10, task:"Code Review", assignedTo:"Ankit", priority:"Medium", status:"Completed"},
  {id:11, task:"Performance Check", assignedTo:"Vikas", priority:"Low", status:"Pending"},
  {id:12, task:"Security Audit", assignedTo:"Rohit", priority:"High", status:"In Progress"},
  {id:13, task:"UI Testing", assignedTo:"Sneha", priority:"Medium", status:"Completed"},
  {id:14, task:"Cloud Setup", assignedTo:"Pooja", priority:"High", status:"Pending"},
  {id:15, task:"Mobile Support", assignedTo:"Deepak", priority:"Low", status:"Completed"},
  {id:16, task:"Bug Analysis", assignedTo:"Mohit", priority:"Medium", status:"In Progress"},
  {id:17, task:"Feature Update", assignedTo:"Nikita", priority:"High", status:"Completed"},
  {id:18, task:"Release Planning", assignedTo:"Yash", priority:"Medium", status:"Pending"},
  {id:19, task:"Final Testing", assignedTo:"Aditya", priority:"High", status:"Completed"},
  {id:20, task:"Project Report", assignedTo:"Ayesha", priority:"Low", status:"Pending"}
]


// ================= CUSTOMER SUPPORT TICKETS =================

const ticketColumns = [
  { title:"Ticket ID", key:"ticketId" },
  { title:"Customer", key:"customer" },
  { title:"Issue", key:"issue" },
  { title:"Status", key:"status" }
]


const tickets = [
  {id:1, ticketId:"T001", customer:"Rajat", issue:"Login Problem", status:"Open"},
  {id:2, ticketId:"T002", customer:"Rahul", issue:"Payment Failed", status:"Closed"},
  {id:3, ticketId:"T003", customer:"Amit", issue:"Account Issue", status:"Open"},
  {id:4, ticketId:"T004", customer:"Neha", issue:"Password Reset", status:"Resolved"},
  {id:5, ticketId:"T005", customer:"Priya", issue:"App Crash", status:"Open"},
  {id:6, ticketId:"T006", customer:"Arjun", issue:"Refund Request", status:"Pending"},
  {id:7, ticketId:"T007", customer:"Karan", issue:"Order Delay", status:"Closed"},
  {id:8, ticketId:"T008", customer:"Riya", issue:"Subscription", status:"Resolved"},
  {id:9, ticketId:"T009", customer:"Simran", issue:"Verification", status:"Open"},
  {id:10, ticketId:"T010", customer:"Ankit", issue:"Payment Error", status:"Pending"},
  {id:11, ticketId:"T011", customer:"Vikas", issue:"Service Issue", status:"Resolved"},
  {id:12, ticketId:"T012", customer:"Rohit", issue:"Technical Error", status:"Open"},
  {id:13, ticketId:"T013", customer:"Sneha", issue:"Account Lock", status:"Closed"},
  {id:14, ticketId:"T014", customer:"Pooja", issue:"Invoice Issue", status:"Pending"},
  {id:15, ticketId:"T015", customer:"Deepak", issue:"App Update", status:"Resolved"},
  {id:16, ticketId:"T016", customer:"Mohit", issue:"Server Error", status:"Open"},
  {id:17, ticketId:"T017", customer:"Nikita", issue:"Profile Update", status:"Closed"},
  {id:18, ticketId:"T018", customer:"Yash", issue:"Order Cancellation", status:"Pending"},
  {id:19, ticketId:"T019", customer:"Aditya", issue:"Delivery Issue", status:"Resolved"},
  {id:20, ticketId:"T020", customer:"Ayesha", issue:"Refund Delay", status:"Open"}
]

</script>