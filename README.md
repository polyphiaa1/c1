# c1
common cold

globals [
  driver-seat     ; driver's seat
  door            ; door
  virus-speed     ; speed of the virus particles
]
turtles-own [
  infected?  ; Track whether a person is infected
]
to setup
  clear-all
  resize-world -10 10 -26 26

  set virus-speed 0.1 ; Adjust the speed of the virus particles as needed

  draw-layout
  create-people
  create-virus
  reset-ticks
end




to create-people ; para mapunta sila sa patch
  let infected-people 5  ; Number of infected people
  repeat infected-people [
    let location one-of patches with [pcolor = gray]
    ask location [
  ask patches with [pcolor = gray] [
    sprout 1 [
      set size 2 ; for people size adjustmet
      set color yellow;
      set shape "person" ; Adjust shape as needed
    ]
    ]
    ]
  ]
end

to create-virus
  repeat 20 [
    create-virus-particle
  ]
end

to create-virus-particle
  crt 1 [
    setxy random-xcor random-ycor
    set size 1
    set shape "circle"
    set color red
  ]
end

to move-virus
  ask turtles with [shape = "circle"] [
    right random 360
    forward virus-speed
    if xcor > 10 or xcor < -10 or ycor > 26 or ycor < -26 [
      set heading towards one-of patches with [pcolor = gray]
    ]
  ]
end

to simulate-common-cold
  move-virus
  ; Add any additional actions related to the common cold simulation here
  tick
end

to draw-layout
  let x-center 0
  let y-center 0

  ; Left seats (14)
  let left-x x-center - 6
  let left-y y-center + 14
  repeat 14 [
    create-seat left-x left-y
    set left-y left-y - 2.5 ; 
  ]

  ; Middle seats (3)
  let middle-x x-center + 1
  let middle-y y-center + 10
  create-middle middle-x middle-y

  let middle-1 x-center + 1
  let middle-2 y-center - 1
  create-middle middle-1 middle-2

  let middle-3 x-center + 1
  let middle-4 y-center - 10
  create-middle middle-3 middle-4

  ; Right seats (14)
  let right-x x-center + 6
  let right-y y-center + 18
  set right-y right-y + 2 ; 4 seats
  repeat 4 [
    create-seat right-x right-y
    set right-y right-y - 2.5 ; spacing between seats
  ]

  ; 10 seats on the right
  set right-y right-y - 6 ; additional space after front 4 seats
  repeat 10 [
    create-seat right-x right-y
    set right-y right-y - 2.5 ; spacing between seats
  ]

  ; Create the driver's seat
  create-driver-seat x-center - 6 y-center + 20

  ; Create door
  create-door x-center + 8 y-center + 5.9

  ; Create closed windows
  create-closed-windows

  ; Create the back side of the bus
  create-back-side

  ; Create the front side of the bus
  create-front-window
end

to create-seat [x y]
  ask patch x y [
    set pcolor gray
  ]
  crt 1 [
    setxy x y
    set size 5
    set shape "rect3"
    set label "" ; Remove turtle label
  ]
end

to create-middle [x y]
  ask patch x y [
    set pcolor gray
  ]
  crt 1 [
    setxy x y
    set size 5
    set shape "mid"
    set label "" ; 
  ]
end

to create-driver-seat [x y]
  ask patch x y [
    set pcolor gray
  ]
  crt 1 [
    setxy x y
    set size 5
    set shape "rect4"
    set label "Driver"
  ]
end

to create-door [x y]
  crt 1 [
    setxy x y
    set color red
    set size 17
    set shape "d1"
  ]
end

to create-closed-windows
  ; Closed windows on the left side
  let left-x -19.6
  let left-y 19
  repeat 10 [
    create-window left-x left-y
    set left-y left-y - 5 ; spacing between windows
  ]

  ; Closed windows on the right side
  let right-x 20.35
  let right-y -2.2
  repeat 10 [
    create-window right-x right-y
    set right-y right-y - 3 ; spacing between windows
  ]
end

to create-window [x y]
  crt 1 [
    setxy x y
    set size 39.6
    set shape "w1"
    set label "" ; Remove turtle label
  ]
end

to create-back-side
  ; Closed back side of the bus
  let back-x -19.6
  let back-y -20
  repeat 5 [
    create-back-window back-x back-y
    set back-x back-x + 10 ; spacing between back windows
  ]
end

to create-back-window [x y]
  crt 1 [
    setxy x y
    set size 35
    set shape "b1"
    set label "" ; Remove turtle label
  ]
end

to create-front-window
  ; Closed front side of the bus
  let front-x -19.6
  let front-y 26
  repeat 5 [
    create-front-window-turtle front-x front-y
    set front-x front-x + 10 ; spacing between front windows
  ]
end

to create-front-window-turtle [x y]
  crt 1 [
    setxy x y
    set size 12
    set shape "b1"
    set label "" ; Remove turtle label
  ]
end
