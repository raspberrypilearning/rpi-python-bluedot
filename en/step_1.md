To begin using Blue Dot, you will need to pair your Android device with your Raspberry Pi.

#### On your Android device:
- Open **Settings**.
- Select **Bluetooth** and turn it on to make your device discoverable.
  ![available devices](images/available_devices.png)

#### On your Raspberry Pi:
- Click on the **Bluetooth** icon in the task bar.
- Turn on Bluetooth.
- Click on **Make Discoverable**.
  ![make discoverable](images/make_discoverable.png)
- Click **Add Device**.
- Your Android device should appear in the list. Select it and click **Pair**.
  ![add device](images/add_device.png)
  
- You will then be prompted to accept, or to input a PIN (personal identification number). Once you've done this, your devices should be paired.

	![confirm pair](images/confirm_pair.png)
	![pairing code](images/pairing_code.png)
	![pair success](images/pair_success.png)

### Receiving signals with Python

You can now use the `bluedot` Python module to receive messages from the Android app.

- On your Raspberry Pi, open **mu** from the **Programming** menu to write the following simple program.

	```python
	from bluedot import BlueDot
	bd = BlueDot()
	bd.wait_for_press()
	print("You pressed the blue dot!")
	```

- Save and run the code.
- On your Android device, open the Blue Dot app and select your Raspberry Pi from the list of available devices.
	![bd devices](images/bd_devices.png)
	![bd_connected](images/bd_connected.png)
- In the Python shell, you should see a message telling you that the device has connected.
  ![connected](images/connected.png)
- Push the blue dot on the Android screen, and the message `You pressed the blue dot!` will appear in the shell.

### More methods

- The following additional methods can be used to receive more information about how you are interacting with the blue dot.

	```python
	bd.when_pressed = foo ##run the function foo when the blue dot is pressed
	bd.when_release = bar ##run the function bar when the blue dot is released
	bd.when_moved = baz ##run the function baz when your finger moves on the blue dot
	```

- When the functions are called, the position of your finger on the blue dot will be passed into the function. An example `foo` function might look like this:

	```python
	def foo(pos):
		print(pos.x)
		print(pos.y)
	```

- This will provide you with the `x` and `y` coordinates of the finger on the blue dot (from -1 to 1).

- Additionally, `pos.top` would return `True` if the finger press was near the top of the blue dot. Similarly, `pos.bottom`, `pos.right` and `pos.left` can be used.
