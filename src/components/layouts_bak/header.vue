<template>
  <header id="header">
    <div id="logo-group">

      <!-- PLACE YOUR LOGO HERE -->
      <!--<span id="logo"> <img src="/static/admin/core/img/logo.png" alt="SmartAdmin"> </span>-->
      <!-- END LOGO PLACEHOLDER -->

      <!-- Note: The activity badge color changes when clicked and resets the number to 0
                   Suggestion: You may want to set a flag when this happens to tick off all checked messages / notifications -->
      <!--<span id="activity" class="activity-dropdown"> <i class="fa fa-user"></i> <b class="badge"> 21 </b> </span>-->

      <!-- AJAX-DROPDOWN : control this dropdown height, look and feel from the LESS variable file -->
      <div class="ajax-dropdown active">

        <!-- the ID links are fetched via AJAX to the ajax container "ajax-notifications" -->
        <div class="btn-group btn-group-justified" data-toggle="buttons">
          <label class="btn btn-default">
            <input type="radio" name="activity" id="ajax/notify/mail.html">
            Msgs (14) </label>
          <label class="btn btn-default">
            <input type="radio" name="activity" id="ajax/notify/notifications.html">
            notify (3) </label>
          <label class="btn btn-default">
            <input type="radio" name="activity" id="ajax/notify/tasks.html">
            Tasks (4) </label>
        </div>

        <!-- notification content -->
        <div class="ajax-notifications custom-scroll">

          <div class="alert alert-transparent">
            <h4>Click a button to show messages here</h4>
            This blank page message helps protect your privacy, or you can show the first message here automatically.
          </div>

          <i class="fa fa-lock fa-4x fa-border"></i>

        </div>
        <!-- end notification content -->

        <!-- footer: refresh area -->
        <span> Last updated on: 12/12/2013 9:43AM
						<button type="button" data-loading-text="<i class='fa fa-refresh fa-spin'></i> Loading..."
                    class="btn btn-xs btn-default pull-right">
							<i class="fa fa-refresh"></i>
						</button> </span>
        <!-- end footer -->

      </div>
      <!-- END AJAX-DROPDOWN -->
    </div>


    <!-- #TOGGLE LAYOUT BUTTONS -->
    <!-- pulled right: nav area -->
    <div class="pull-right">

      <!-- collapse menu button -->
      <div id="hide-menu" class="btn-header pull-right">
        <span> <a href="javascript:void(0);" data-action="toggleMenu" title="Collapse Menu"><i
          class="fa fa-reorder"></i></a> </span>
      </div>
      <!-- end collapse menu -->


      <!-- logout button -->
      <div id="logout" class="btn-header transparent pull-right">
        <span> <router-link to="/login"><i class="fa fa-sign-out"></i></router-link> </span>
      </div>
      <!-- end logout button -->

      <!-- end search mobile button -->

      <!-- #SEARCH -->
      <!-- end input: search field -->

      <!-- #Voice Command: Start Speech -->

      <!-- end voice command -->


    </div>
    <!-- end pulled right: nav area -->

  </header>
</template>
<style lang="scss" scoped>


</style>
<script type="text/javascript">
  export default{
    data(){
      return {}
    }
  }


</script>
