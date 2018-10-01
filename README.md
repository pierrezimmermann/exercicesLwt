# exercicesLwt



let rec alarme_inf f s =
  	let%lwt () = Lwt_unix.sleep f in
  	print_endline s ;
  	alarme_inf f s

let rec alarmes_async () =
  	let p_1 =
    	let%lwt () = Lwt_unix.sleep 5.0 in
    	print_endline "a";
    	Lwt.return_unit

  	in

  	let p_2 =
    	let%lwt () = Lwt_unix.sleep 3.0 in
    	print_endline "b";
    	Lwt.return_unit

  	in

  	let p_3 =
    	let%lwt () = Lwt_unix.sleep 10.0 in
    	print_endline "c";
    	Lwt.return_unit

  	in

  	let%lwt () = Lwt.join [ p_1;p_2;p_3] in
  	alarmes_async()





let alarmes_rand () =
  	Random.self_init () ;
  	let p_1 =
    	let x = float_of_int (Random.int 10) in
    	let%lwt () = Lwt_unix.sleep x in
    	print_endline "a";
    	Lwt.return_unit

  	in

  	let p_2 =
    	let x = float_of_int (Random.int 10) in
    	let%lwt () = Lwt_unix.sleep x in
    	print_endline "b";
    	Lwt.return_unit


  in

  let p_3 =
    	let x = float_of_int (Random.int 10) in
    	let%lwt () = Lwt_unix.sleep x in
    	print_endline "c";
    	Lwt.return_unit
  in

  Lwt.join [ p_1; p_2; p_3]


let alarme_rand () =
  	let%lwt () = Lwt_unix.sleep (float_of_int (Random.int 20)) in
  	print_endline "a" ;
    Lwt.return_unit



let rec alarmes_inf () =
    let p_1 =
    	alarme_inf 5. "a"
    in
  	let p_2 =
    	alarme_inf 3. "b"
	in
  	let p_3 =
    	alarme_inf 2. "c"

  	in

  	Lwt.join [p_1;p_2;p_3]


let () = Lwt_main.run @@ alarmes_inf ()
