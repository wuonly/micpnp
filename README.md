# micpnp
pull and push  with jquery

//TODO write a plugin later
		var starty = 0;
		var movedy = 0;
		$('#main-comment').on(
				'touchstart',
				function(ev) {
					$('<div id="pullheader" class="text-center"><div>').insertBefore($('#main-comment'))
				});
		$('#main-comment').on('touchmove', function(event) {
			if (starty == 0)
				starty = event.originalEvent.changedTouches[0].clientY;
			movedy = event.originalEvent.changedTouches[0].clientY - starty;
			if (movedy < 20) {
				$("#pullheader").text("");
			} else if (movedy < 50) {
				$("#pullheader").text("下拉刷新");
			} else if (movedy >= 50) {
				$("#pullheader").text("松开刷新");
			}
			$("#pullheader").css("height",movedy);
		});
		$('#main-comment').on('touchend', function(ev) {
			if (movedy >= 50) {
				loadComments(0);
			}
			starty = 0;
			movedy = 0;
			$("#pullheader").remove();
		});
