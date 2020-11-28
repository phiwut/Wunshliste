<script>
  import * as jquery from "jquery";

  let wishList = [
    {
      title: "Write my first post",
      description: "fgddg",
      imgURL: "https://abc.xyz",
      status: true,
      id: ""
    },
    {
      title: "Upload the post to the blog",
      description: "",
      imgURL: "",
      status: false,
      id: ""
    },
    {
      title: "Publish the post at Facebook",
      description: "",
      imgURL: "",
      status: false,
      id: ""
    }
  ];

  const token = "Token 6fd7dafb-a2da-4812-9a35-6029d017e29c"; // Since this will be public anyway I don't care if someone sees my key

  function initializeWishlist() {
    wishList.forEach(wish => {
      if ((wish.id = "")) {
        wish.id = createBoolean(wish.title);
      }

      wish.status = getStatus(wish.id);
    });

    console.log(wishList);
  }

  function createBoolean(label) {
    jquery.ajax({
      type: "POST",
      beforeSend: function(request) {
        request.setRequestHeader("Authorization", token);
      },
      url: "https://api.booleans.io",
      data: '{"value": false, "label": "' + label + '"}',
      processData: false,
      success: function(msg) {
        console.log("POST successfull:");
        console.log(msg);
        return msg.id;
      },
      error: function(msg) {
        console.error("POST error (" + label + ")");
        console.error(msg);
      }
    });
  }

  function getStatus(id) {
    jquery.ajax({
      type: "GET",
      beforeSend: function(request) {
        request.setRequestHeader("Authorization", token);
      },
      url: "https://api.booleans.io/" + id,
      processData: false,
      success: function(msg) {
        console.log("GET successfull:");
        console.log(msg);
        return msg.value;
      },
      error: function(msg) {
        console.error("GET error (" + id + ")");
        console.error(msg);
      }
    });
  }

  function toggle(id) {
    let currentStatus = getStatus(id);

    jquery.ajax({
      type: "PATCH",
      beforeSend: function(request) {
        request.setRequestHeader("Authorization", token);
      },
      url: "https://api.booleans.io/" + id,
      data: '{"value": ' + !currentStatus + '"}',
      processData: false,
      success: function(msg) {
        console.log("PATCH successfull:");
        console.log(msg);
        return msg.value;
      },
      error: function(msg) {
        console.error("PATCH error (" + id + ")");
        console.error(msg);
      }
    });
  }

  initializeWishlist();
</script>

{#each wishList as wish, index}
	<span class:checked={wish.status}>{wish.title}</span>
	<input bind:checked={wish.status} type="checkbox">
	<br/>
{/each} 


<style>
  .checked {
    text-decoration: line-through;
  }
</style> 