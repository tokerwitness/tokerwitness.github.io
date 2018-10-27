
<html>
<head>
<meta charset="utf-8" />
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width">
<meta http-equiv="refresh" content="300">
<title>Smoke.io Witnesses</title>
<meta name="msapplication-TileColor" content="#FFFFFF" />
<link href="https://fonts.googleapis.com/css?family=Lato:300,400,600,700,900" rel="stylesheet" type="text/css" />
<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.2.4/jquery.min.js"></script>
<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/jqueryui/1.12.1/jquery-ui.min.js"></script>
<link ref="stylesheet" type="text/css" href="https://cdnjs.cloudflare.com/ajax/libs/jqueryui/1.12.1/jquery-ui.min.css">
<link rel="stylesheet" type="text/css" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.6.3/css/font-awesome.min.css">
<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.14.1/moment.min.js"></script>
<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/bignumber.js/2.4.0/bignumber.min.js"></script>

<style>body {font-size:11pt; font-family:"Calibri","sans-serif";}</style>

<script>
var WebSocketWrapper;
WebSocketWrapper = function() {
	var ws = WebSocketWrapper.prototype;

	function WebSocketWrapper(server) {
		this.server = server;
		this.connection = {};
		this.callbacks = [];
	}
	ws.connect = function() {
		var _this = this;

		return new Promise(function(resolve, reject) {
			if('WebSocket' in window) {
				_this.connection = new WebSocket(_this.server);
				_this.connection.onopen = function() {
					resolve(_this.connection);
				};
				_this.connection.onerror = function(error) {
					reject(Error('Error connecting to server, please reload the page!' + error));
				};
				_this.connection.onmessage = function(data) {
					var sdata = JSON.parse(data['data']);
					_this.callbacks[sdata['id']](sdata['result']);
				};
			} else {
				reject(Error('Your browser is too old, please get a recent one!'));
			}
		});
	};
	ws.send = function(data, callback) {
		this.callbacks[data['id']] = callback;
		var json = JSON.stringify(data);
		this.connection.send(json);
	};
	return WebSocketWrapper;
}();
var SteemWrapper;
SteemWrapper = function() {
	var steem = SteemWrapper.prototype;

	function SteemWrapper(ws) {
		this.ws = ws;
		this.id = 0;
	}
	steem.send = function(method, params, callback) {
		++this.id;
		var data = {
			"id": this.id,
			"method": method,
			"params": params
		};
		this.ws.send(data, callback);
	};
	return SteemWrapper;
}();

var next_shuffle_block_num = 0;
var current_virtual_time = 0;
var last_block_number = 0;
var last_virtual_time = 0;
//var last_miner_queue = "";
var witness_rank = [];

function main() {

//var server = 'wss://steemd.privex.io';
var server = 'ws://51.158.79.144:8090';
var ws = new WebSocketWrapper(server);

ws.connect().then(function(response) {
	console.log(response);
	var steem = new SteemWrapper(ws);

	var wsocketblock = function() {
		steem.send('get_dynamic_global_properties', [], function(globprops) {

			var block_number = globprops["head_block_number"];
			var witness = globprops["current_witness"];
			var time = moment().format('LTS');

			if(last_block_number != block_number) {
				last_block_number = block_number;

				$(".witness:not(.highlighted)").css("color", "").css("font-weight", "");
				$("._witnessed").css("opacity", "0.3");
				$("[id='witness_" + witness + "']").find(".blocknum").html(block_number);
				$("[id='witness_" + witness + "']").addClass("_witnessed").css("color", "green").css("font-weight", "bold");
				
				if(next_shuffle_block_num != 0) {
					var diff = next_shuffle_block_num - block_number;
					if(diff == 0) $('#shuffle').html('&middot;');
					else $('#shuffle').html('<em><small>-' + diff + '</small></em>');
				}
			}

			document.title = block_number + ' ' + witness + ' [' + time + ']';

			setTimeout(wsocketblock, 750);
		});
	};

	
	var wsschedule = function() {
		steem.send('get_witness_schedule', [], function(schedule) {
			current_virtual_time = schedule["current_virtual_time"];
			next_shuffle_block_num = schedule["next_shuffle_block_num"];
			var current = schedule["current_shuffled_witnesses"];

			var refreshed = moment().format('LTS');

			// currently using get_active_witnesses while get_witness_schedule is broken
			/*var list = "";
			for(var i = 0; i < current.length; i++) {
				var style = '';

				list += '<div id="witness_' + current[i] + '" class="witness" style="position:relative;">';
				list += '<span class="rank" style="position:absolute; left:0; font-style:italic; font-size:small;">.</span>';
				list += '<span' + style + '>' + current[i] + </span>';
				list += '<span class="missed">.</span>';
				list += '<span class="blocknum" style="position:absolute; right:0;"></span></div>';
			}*/

			if(last_virtual_time != current_virtual_time) {
				var delay = 0;
				if(last_virtual_time != 0) delay = 1800;

				last_virtual_time = current_virtual_time;

				setTimeout(function() {
					var code = '<div style="text-align:center;">--- <em><small>refreshed @ ' + refreshed + '</small></em> ---</div>';
					code += '<div style="line-height:0.7em;"><br></div>';
					code += '<div id="list">' + list + '</div><br>';
					code += '<div style="position:relative;">' + next_shuffle_block_num + '<div style="position:absolute; top:0; width:100%; padding-left:5em;" id="shuffle"></div></div>';
					code += '<div><em><small>(next_shuffle_block_num)</small></em></div><div style="line-height:0.5em;"><br></div>';
					code += '<div>' + current_virtual_time + '</div>';
					code += '<div><em><small>(current_virtual_time)</small></em></div>';
					$("#consoleschedule").html(code);
				}, delay);
			}

			//setTimeout(wsschedule, 1000);
			setTimeout(wsactive, 1000);
		});
	};

	var list = "";
	// a separate call to get the list of current shuffled witnesses, can remove after get_witness_schedule is fixed
	var wsactive = function() {
		steem.send('get_active_witnesses', [], function(witnesses) {
			list = "";
			for(var i = 0; i < witnesses.length; i++) {
				if(witnesses[i] == "") continue; // current bug in response

				var style = '';

				list += '<div id="witness_' + witnesses[i] + '" class="witness" style="position:relative;">';
				list += '<span class="rank" style="position:absolute; left:0; font-style:italic; font-size:small;">.</span>';
				list += '<span ' + style + '>' + witnesses[i] + '</span>';
				list += '<span class="missed"></span>';
				list += '<span class="blocknum" style="position:absolute; right:0;"></span></div>';
			}

			wsschedule();
		});
	};

	/*var wsminers = function() {
		steem.send('get_miner_queue', [], function(queue) {

			var refreshed = moment().format('LTS');

			if(last_miner_queue != queue.join()) {
				last_miner_queue = queue.join();

				var code = '<div style="text-align:center;">--- <em><small>refreshed @ ' + refreshed + '</small></em> ---</div>';
				code += '<div style="line-height:0.7em;"><br></div>';
				for(var i = 0; i < queue.length; i++) {
					var style = '';
					if(queue[i].startsWith('supercomputing') || queue[i].startsWith('rabbit') || queue[i].startsWith('aizen') || queue[i].startsWith('hagie') || queue[i].startsWith('yme') || queue[i].startsWith('perezoso') || queue[i].startsWith('itsmine') || queue[i].startsWith('bento') || queue[i].startsWith('notbad') || queue[i].startsWith('gtx-1080-sc') || queue[i].startsWith('hamster') || queue[i].startsWith('ribozyme') || queue[i].startsWith('twiggy') || queue[i].startsWith('ganymede') || queue[i].startsWith('tammy') || queue[i].startsWith('birte') || queue[i].startsWith('berit') || queue[i].startsWith('hare') || queue[i].startsWith('smallhands') || queue[i].startsWith('kerstin') || queue[i].startsWith('kartoffel') || queue[i].startsWith('esther'))
						true; else style = 'zcolor:orange;';					code += '<div id="miner_' + queue[i] + '" class="miner" style="position:relative;' + style + '">';
					code += '<span class="rank" style="position:absolute; left:0; font-style:italic; font-size:small;">' + ((i < 99) ? "&nbsp; " : "") + ((i < 9) ? "&nbsp; " : "") + '(' + (i + 1) + ')</span>';
					code += '<span class="miner">' + queue[i] + '</span></div>';
				}
				$("#consoleminers").html(code);
				//$("#totalminers").html('<a href="data:text/plain,' + encodeURIComponent(queue.sort().join("\n")) + '" target="_blank">' + queue.length + ' total</a>');
				$("#totalminers").html('<a href="view/?' + encodeURIComponent('[Generated on ' + moment().format('l LTS') + "]\n\n" + queue.sort().join("\n")) + '" target="_blank">' + queue.length + ' total</a>');
			}

			setTimeout(wsminers, 1000);
		});
	};*/


	var first = true;

	var wswitnesses = function() {

		witness_rank = [];

		steem.send('get_witnesses_by_vote', ["", "100"], function(witness) {
			for(var i = 0; i < witness.length; i++) {
				var owner = witness[i]['owner'];
				var missed = witness[i]['total_missed'];
				/*var votes = witness[i]['votes'];
				var virtual_last_update = witness[i]['virtual_last_update'];
				var virtual_position = witness[i]['virtual_position'];*/
				var virtual_scheduled_time = witness[i]['virtual_scheduled_time'];
				var signing_key = witness[i]['signing_key'];
				witness_rank.push({'rank': (i + 1), 'owner': owner, 'missed':missed, 'virtual_scheduled_time': virtual_scheduled_time, 'signing_key': signing_key});
			}

						
			updateWitnessesList();
			setTimeout(wswitnesses, 1000);
			
			
		});
	};

	//wsschedule();
	wsactive();
	wsocketblock();
	//wsminers();
	wswitnesses();

});

}

function updateWitnessesList() {

	var refreshed = moment().format('LTS');

	var code = '<div style="position:relative;"><span style="position:absolute; left:0;">--- <em><small>refreshed @ ' + refreshed + '</small></em> ---</span><span>&nbsp;</span>';
	code += '<span style="position:absolute; right:0;"><em>(virtual_scheduled_time diff)</em></span></div><div style="line-height:0.7em;"><br></div>';

	witness_rank.sort(function(a, b) {
		if(a.virtual_scheduled_time < b.virtual_scheduled_time) return -1;
		if(a.virtual_scheduled_time > b.virtual_scheduled_time) return 1;
		return 0;
	});

	var index = 0;
	for(var i = 0; i < witness_rank.length; i++) {
		var rank = witness_rank[i]['rank'];
		var owner = witness_rank[i]['owner'];
		var missed = witness_rank[i]['missed'];
		/*var votes = witness_rank[i]['votes'];
		var virtual_last_update = witness_rank[i]['virtual_last_update'];
		var virtual_position = witness_rank[i]['virtual_position'];*/
		var virtual_scheduled_time = witness_rank[i]['virtual_scheduled_time'];
		var signing_key = witness_rank[i]['signing_key'];

		var style = "";

		if(rank <= 12) {
			style = "display:none;";
			$("[id='witness_" + owner + "']").find(".rank").html(((rank <= 12) ? "&nbsp; " : "") + "(" + rank + ")");
			$("[id='witness_" + owner + "']").find(".missed").html(" (" + missed + ")");
		}
		else {
			$("[id='witness_" + owner + "']").find(".rank").html('(' + rank + ') <span style="font-style:normal;">backup</span>');
			$("[id='witness_" + owner + "']").find(".missed").html(" (" + missed + ")");
			if(signing_key != 'STM1111111111111111111111111111111114T1Anm') index++;
		}
		
		if(signing_key != 'STM1111111111111111111111111111111114T1Anm') {
			code += '<div id="witness_rank_' + owner + '" class="witness_rank" style="position:relative;' + style + '">';
			code += '<span class="rank0" style="position:absolute; left:0;"><em><small>' + ((rank < 100) ? "&nbsp; " : "") + ((rank < 10) ? "&nbsp; " : "") + '(' + rank + ')</small></em> &nbsp; ';
			code += '<span class="owner">' + owner + '</span><span> (' + missed + ')</span>' + '</span><span>&nbsp;</span>';
			var x = new BigNumber(virtual_scheduled_time);var y = new BigNumber(current_virtual_time);var diff = x.sub(y).toFixed();code += '<span class="scheduled" style="position:absolute; right:0;">' + diff;if(rank <= 20) code += ' &nbsp; <em><small>[' + ((index >= 10) ? '&nbsp; ' : '') + '&nbsp; ]</small></em>' + ((index < 10) ? ' &nbsp;' : '') + ((index < 100) ? ' &nbsp;' : '');else code += ' &nbsp; <em><small>[' + index + ']</small></em>' + ((index < 10) ? ' &nbsp;' : '') + ((index < 100) ? ' &nbsp;' : '');code += '</span></div>';		}

		//$(".rank:contains('.')").html('&nbsp; (&middot;) <span style="font-style:normal;">miner</span>');

		$("#consolewitnesses").html(code);

	}
}

$(function() {
	if(window.WebSocket) {
		main();
	}
	else {
		alert('You need a modern browser supporting websockets for this');
	}
});

</script>

</head>
<body>

<img src='whaleshares.jpg' style='position: fixed; top: 0px; z-index: -1' />

<br>

<style>

button {
  -webkit-appearance: none;
  -webkit-user-select: none;
  background-image: -webkit-linear-gradient(#ededed, #ededed 38%, #dedede);
  border: 1px solid rgba(0, 0, 0, 0.25);
  border-radius: 2px;
  box-shadow: 0 1px 0 rgba(0, 0, 0, 0.08),
      inset 0 1px 2px rgba(255, 255, 255, 0.75);
  color: #444;
  font: inherit;
  margin: 0 1px 0 0;
  outline: none;
  text-shadow: 0 1px 0 rgb(240, 240, 240);
}

button {
  min-height: 2em;
  min-width: 4em;
/* The following platform-specific rule is necessary to get adjacent
   * buttons, text inputs, and so forth to align on their borders while also
   * aligning on the text's baselines. */
  padding-bottom: 1px;
}

button {
  -webkit-padding-end: 10px;
  -webkit-padding-start: 10px;
}

button:hover {
  background-image: -webkit-linear-gradient(#f0f0f0, #f0f0f0 38%, #e0e0e0);
  border-color: rgba(0, 0, 0, 0.3);
  box-shadow: 0 1px 0 rgba(0, 0, 0, 0.12),
      inset 0 1px 2px rgba(255, 255, 255, 0.95);
  color: black;
}

button:active {
  background-image: -webkit-linear-gradient(#e7e7e7, #e7e7e7 38%, #d7d7d7);
  box-shadow: none;
  text-shadow: none;
}

button:disabled {
  background-image: -webkit-linear-gradient(#f1f1f1, #f1f1f1 38%, #e6e6e6);
  border-color: rgba(80, 80, 80, 0.2);
  box-shadow: 0 1px 0 rgba(80, 80, 80, 0.08),
      inset 0 1px 2px rgba(255, 255, 255, 0.75);
  color: #aaa;
}

button:focus {
  /* OVERRIDE */
  -webkit-transition: border-color 200ms;
  /* We use border color because it follows the border radius (unlike outline).
   * This is particularly noticeable on mac. */
  border-color: rgb(77, 144, 254);
  outline: none;
}

button img {width:16px; height:16px; vertical-align:middle; border:0;}
button span {vertical-align:middle;}


button {margin:1em; font-weight:bold; color:#17365D;}

</style>

<center>
<span style="display:inline-block;">

<h1><center>Smoke.io Witness Schedule</center></h1>

<span style="display:inline-block; border:1px dotted #4F81BD; min-width:24em; background: lightgrey; padding:1em; margin:1em; vertical-align:top">
<span style="font-size:medium; font-weight:bold; color:#4F81BD">Witness Schedule</span>
<div id="consoleschedule" style="margin:0.7em 0;">...</div>
</span>

<span style="display:inline-block; border:1px dotted #4F81BD; min-width:32em; background: lightgrey; padding:1em; margin:1em; vertical-align:top; position:relative;">
<span style="font-size:medium; font-weight:bold; color:#4F81BD">Backup Witnesses</span><div style="position:absolute; top:0.2em; left:0.5em; text-align:left; line-height:1.1em;"><!-- <a href="/whale/?c=show200" style="color:black; font-size:0.8em; font-style:italic;">Show top 200</a><br><a href="/whale/?c=includetop20" style="color:black; font-size:0.8em; font-style:italic;">Include top 20</a></div><div style="position:absolute; top:0.2em; right:0.5em;"><a href="/whale/?c=showabstime" style="color:black; font-size:0.8em; font-style:italic;">Show absolute time</a>--></div><div id="consolewitnesses" style="margin:0.7em 0;">...</div>
</span>


</span>
</center>

</body>
</html>
