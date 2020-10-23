# Functionality

This file will explain what is the expected functionality.

## Overview

Main reason I decided to create this thing is because I like to know what is going on in my vehicles.
Even that I'm investigating all indications on that something can be wrong, it is not possible to know state of whole system.
Especially if you don't have all, possible to gather, data. But even if you know every variable in real-time.
Some times it is just not possible to catch every abnormal sensor reading or increased vibration of some element.

Thats why gathering that data and analyzing it can be really helpful when it comes to monitoring for all possible incoming failures.
But because limitations of cheap embedded systems not all data can be stored, at least not for long periods of time.
In that circumstances some data processing have to be considered.

## Sensor data acquisition

Types of data that are planned to be read, with proposed types of sensor:

- Humidity
- **Temperature**
  - **Engine oil temperature** R: up to 150 centigrade; P: all Pt1000 sensors with extension cables
  - **Ambient and/or intake temperature** R: Range at least from -25 to 80 centigrade; P: all Pt1000 sensors with extension cables
- **Voltage**
  - **Battery** R: Up to ~18VDC, low freq
  - **Voltage spikes from ignition cables** R: All sensor lines with the same length, async edge triggered
  - Gear signals (up to 7, but just 1 will be really needed [neutral])
  - Hijacked speed sensor signals (investigate this)
- **Kinematics**
  - **Vibration of engine block** R: min. 25kHz (not possible?) [Studies on contact microphones](https://pdf.sciencedirectassets.com/282173/1-s2.0-S2212827113X00101/1-s2.0-S2212827113006586/main.pdf?X-Amz-Security-Token=IQoJb3JpZ2luX2VjEA8aCXVzLWVhc3QtMSJIMEYCIQCY23Qa%2BR10p56n2YHWKDFSNYnM9xm8g0vfgwIJCtl3WAIhAMjiGUWY4HTC%2BO9aaiToGv7EBVwb41hjunD0nQWSfjkfKrQDCFgQAxoMMDU5MDAzNTQ2ODY1IgzSrkwIs%2F%2FBCQwt0zIqkQM6%2FBF17hagaoMUWd9zPthJcPfXlVOiqcoZzWhZptm7nd0DUHAy5peFn%2FTiXSdMduFCCpnRx%2B62zFDRfbpOmJldWazMdehKBSi6owmXEmrGwUTkai1oW%2Bt2hIuEulV5aPGV8oSJPk5mDKl4DX6Cz6ulsiJh8LcDmM6MpCL97LHEmKmHrNA%2BZuvv2LA7Jar%2BDQ6cQr2CVYvqjxDCTgr42JTQK7SS2JHYwU7VJaA4o8G3%2Fmpyu5VohB1nzdHXWWldAzM8rftPdhdUgA0djikj7KSgETySdDFJ8kSKKMJQdReb7TRqTn71WKUT24nwMhX6i4dbDy3IRtq94T9qR09dTK5pc1xB0zsOtPPM6OlISl%2FVYFeUosODFz8CpyKHztT%2F8xKmmNKo8xi5KnXhpbUI34CAyHNVyuwNaDOy9vFGUk7nov4oV3M06YwJObMRWCsx5hCj9x0dQoZ2jMKhcTbW4J4ZJwYb8UsT9fvDU8by%2BD%2BmfFxLCoLCUtzMG5n7wm%2BYYMJhEZQ6m5gyba9mgUJfHCNVvjDflbr8BTrqAR5jkWlWx4BlIexPJPRajFwEUkF489XqLXezA%2FNy1MGVM1Lf2QFgIqujrmyfwlUaITI7wfy2okkCKc45mYbuBMYKzz71Yj%2BfkflxndkxNqJ%2BhQbDNfeYpZiJ3Q0DyHPrucRZu4OpYOCAqleYIu4W5mo7pcUQNpGcVCFbjXza6J0DYFOoMa6rItMctrRftjZqA0jJgSZpaRUionjcbqCE6GUkWNZHTLNro%2BGywMkYSmwf2YRwp%2Bui%2Bl8q8EYlmY3kAWLNAHmjSUojTrPoiG%2F4xn49yS%2FFFp9XSPNwFM%2BJPWVoqOdlO%2Fh8yWgDDw%3D%3D&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20201020T075528Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAQ3PHCVTYSQAJZHLD%2F20201020%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=ab5ab9d797e4d59f20de998a219fc1adda051ded81a1c3d02d3c95ad5d570c13&hash=6a479e3dce4b4b130f229ebea0f4110df3a46f6b95f34a7ac14a85f6b9ee80c2&host=68042c943591013ac2b2430a89b270f6af2c76d8dfd086a07176afe7c76c2c61&pii=S2212827113006586&tid=spdf-d1b95281-a7bf-4489-aaf9-d9337912b33c&sid=5e5d79324124e24e9b7817088224bdc91926gxrqb&type=client)
  - Vibration of chassis
  - **Acceleration of vehicle in direction of travel** R: 50Hz should do
  - **Roll angle** R: 25Hz should do
  - Pitch angle
- **Time** R: resolution for fastest timer should be ~5us, 1ms systick should be ok for rest of a system
