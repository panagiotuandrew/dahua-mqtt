<h1 align="center">Dahua MQTT</h1>
<p align="center">
  <a href="https://docs.docker.com/compose/">
    <img src="https://img.shields.io/badge/docker%20compose-0e4df2" alt="Docker Compose">
  </a>
  <a href="https://opensource.org/licenses/MIT">
    <img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="License: MIT">
  </a>
</p>

> [!IMPORTANT]
> This docker compose file has been only tested with the Dahua VTO2000A, and may not work with other models.

Dahua MQTT publishes ring presses from Dahua Intercoms as MQTT events.

# Environment Variables

- ```VTO_BASE_URL```: Your VTO's IP address
- ```VTO_USER```: Your VTO's username
- ```VTO_PASS```: Your VTO's password
- ```TARGET_INDEX```: The Dahua event index for your apartment
- ```MQTT_URL```: Your MQTT broker's URL, use ``mqtt://localhost`` if on the same device
- ```MQTT_TOPIC```: Your preferred MQTT topic

# Finding your apartment's number
> [!WARNING]
> The apartment number is not the same as the one located in your internal monitor.

To find your apartment's number, log into your VTO's admin page and open the Developer Tools by right clicking and selecting "Inspect" from the list. 
From there, go to the console tab, and paste the code shown below.

```
const res = await fetch('/cgi-bin/eventManager.cgi?action=attach&codes=[All]', {
  credentials: 'include',
});

console.log('status', res.status, res.headers.get('content-type'));

const reader = res.body.getReader();
const decoder = new TextDecoder();

while (true) {
  const { value, done } = await reader.read();
  if (done) break;

  const chunk = decoder.decode(value, { stream: true });
  console.log(chunk);
}
```
Then, press the call button for your apartment and look for an event that looks like this:
```
Code=CallNoAnswered;action=Start;index=9902;data={
   "CallID" : "9",
   "IsEncryptedStream" : false,
   "LockNum" : 2,
   "SupportPaas" : false,
   "TCPPort" : 37777
}
```
> [!NOTE]
> While the event's name may contain ```CallNoAnswered```, it fires immediately when the call button is pressed, not after the call has been ignored.

Your apartment's number is the ```index``` shown there.
