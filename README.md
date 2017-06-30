# Declarative Home Automation

Managing rules in a home automation system can be complex. Wouldn't it be nice
to leverage our knowledge of React to save us the hassle of learning yet another
language or system? Enter react-home.

Here's some example code:

    import React from 'react'
    import {
      Dwelling, Floor, Room, Dimmer, MotionSensor, Scene
    } from 'react-home'

    const FirstFloor = () => (
      <Floor className="first">
        <Room className="kitchen">
          <Dimmer className="overhead" />
          <Dimmer className="counter" />
        </Room>

        <Room className="dining">
          <Dimmer />
        </Room>

        <Room className="entrance">
          <Dimmer />
          <MotionSensor>
            <Active>
              <SetLevel target="Room.entrance Dimmer" value={100} />
            </Active>
            <Inactive>
              <SetLevel target="Room.entrance Dimmer" value={0} />
            </Inactive>
          </MotionSensor>
          <Closet />
        </Room>

        <Scene className="cooking">
          <SetLevel target="Room.kitchen Dimmer" value={100} />
        </Scene>

        <Scene className="eating">
          <SetLevel target="Room.kitchen Dimmer.overhead" value={30} />
          <SetLevel target="Room.kitchen Dimmer.counter" value={0} />
          <SetLevel target="Room.dining Dimmer" value={0} />
        </Scene>
      </Floor>
    )

    const MyHouse = () => (
      <Dwelling>
        <FirstFloor />
      </Dwelling>
    );

    export default MyHouse
