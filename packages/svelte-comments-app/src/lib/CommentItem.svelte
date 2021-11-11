<script>
  export let user;
  export let avatar;
  export let time;
  export let content;
</script>

<div class="flex">
  <img src={avatar} alt="avatar" class="mr-4 w-12 h-12 rounded-full" />
  <div>
    <p>{user}</p>
    <p class="text-sm text-gray-600">{time}</p>
  </div>
  <span class="ml-auto">
    <svg
      xmlns="http://www.w3.org/2000/svg"
      class="w-5 h-5 text-gray-500"
      viewBox="0 0 512 512"
      fill="currentColor"
    >
      <title>Ellipsis Vertical</title>
      <circle cx="256" cy="256" r="48" />
      <circle cx="256" cy="416" r="48" />
      <circle cx="256" cy="96" r="48" />
    </svg>
  </span>
</div>
<p class="py-4 text-gray-600">{content}</p>
