<h1> Xilog 4g API documentation </h1>
Questions? Find us at <a href=mailto:development@ovarro.com> development@ovarro.com </a>

<h1> Xilog 4g Data Access </h1>
The Xilog 4g API provides access to the raw data recorded by the Xilog logger. To use the API third parties must provide an authorization token with each request. 

<h1> Methods </h1>
<ul>
  <li>Logger/All: Returns all logger sites for the access token</li>
  <li>Data/All: Returns all data for site and the given time span</li>
  <li>Data/All: Returns all data for site and the given time span</li>
  <li>Data/DailyStats: Returns statistical data on each channel specified by date time range.</li>
</ul>

<h1>API</h1>
<h2>Logger/All/{token}</h2>
<h3>Purpose</h3>
Returns array of loggers for the access token
<h3>Signature</h3>
<ol>
<li>Endpoint : <a href="https://app-loggervision-logger-prod-uks-001.azurewebsites.net/Logger/All"> https://app-loggervision-logger-prod-uks-001.azurewebsites.net/Logger/All</a>
</li>
<li> Params
  <ul>
    <li>Token: (string - required)</li>
    <ul>
      <li>Access token</li>
    </ul>
  </ul>
</li>
</ol>
<h3>Return Value</h3>
An array of loggers containing serial number and name.
<pre>
[{
  serial: number,
  name: string
}]
</pre>

<h3>Example</h3>

<h2>Data/All/{SerialNumber}/{StartDate}/{EndDate}/{Token}</h2>
<h3>Purpose</h3>
Returns a collection of the raw channel data for the specified Xilog 4g logger. (Max 8 days)
<h3>Signature</h3>
<ol>
<li>Endpoint : <a href="https://app-loggervision-logger-prod-uks-001.azurewebsites.net/Data/All/"> https://app-loggervision-logger-prod-uks-001.azurewebsites.net/Data/All/</a>
</li>
<li> Params
  <ul>
    <li>SerialNumber: (long - required)</li>
    <ul>
      <li>Logger Serial number as dispalyed on device</li>
    </ul>
    <li>StartDate: (string - yyyy-MM-dd HH:mm)</li>
    <ul>
      <li>Date at which to start querying loggers channel data</li>
    </ul>
    <li>EndDate: (string - yyyy-MM-dd HH:mm)</li>
    <ul>
      <li>Date at which to finish querying loggers channel data. (No more than 8 days after start date) </li>
    </ul>
    <li>Token: (string - required)</li>
    <ul>
      <li>Access token</li>
    </ul>
  </ul>
</li>
</ol>
<h3>Return Value</h3>
An object which contains an array of channels each containing an array of the channel data:
<pre>
[{
  channelName: string,
  data: [{
     type: LogType,
     data: [{
        timestamp: string,
        Value: number
     }]
   }]
}]
</pre>
Where LogType = 
<ul>
<li> Average = 8 </li>
<li> Min = 4 </li>
<li> Max = 2 </li>
<li> Standard Deviation = 1 </li> 
</ul>
<h3>Example</h3>

<h2>Data/Channel/{SerialNumber}/{ChannelName}/{StartDate}/ {EndDate}/{Token})</h2>
<h3>Purpose</h3>
Returns a collection of the raw data for the specified Xilog 4g logger and channel name. (Max 8 days)
<h3>Signature</h3>
<ol>
<li>Endpoint : <a href=" https://app-loggervision-logger-prod-uks-001.azurewebsites.net/Data/Channel/">https://app-loggervision-logger-prod-uks-001.azurewebsites.net/Data/Channel/</a>
</li>
<li> Params
  <ul>
    <li>SerialNumber: (long - required)</li>
    <ul>
      <li>Logger Serial number as dispalyed on device</li>
    </ul>
    <li>ChannelName: (string - required)</li>
    <ul>
      <li>Name of the channel to retrieve data from.</li>
    </ul>
    <li>StartDate: (string - yyyy-MM-dd HH:mm)</li>
    <ul>
      <li>Date at which to start querying loggers channel data</li>
    </ul>
    <li>EndDate: (string - yyyy-MM-dd HH:mm)</li>
    <ul>
      <li>Date at which to finish querying loggers channel data. (No more than 8 days after start date) </li>
    </ul>
    <li>Token: (string - required)</li>
    <ul>
      <li>Access token</li>
    </ul>
  </ul>
</li>
</ol>
<h3>Return Value</h3>
An object which contains an array of the loggers channel data:
<pre>
{
  channelName: string,
  data: [{
     type: LogType,
     data: [{
        timestamp: string,
        Value: number
     }]
   }]
}
</pre>
<h3>Example</h3>

<h2>Data/DailyStats/{SerialNumber}/{StartDate}/{EndDate}/{Token}</h2>
<h3>Purpose</h3>
Returns the daily data statistics for the serial number and specified date. 
<h3>Signature</h3>
<ol>
<li>Endpoint : <a href=" https://app-loggervision-logger-prod-uks-001.azurewebsites.net/Data/DailiyStats/">  https://app-loggervision-logger-prod-uks-001.azurewebsites.net/Data/DailiyStats/</a>
</li>
<li> Params
  <ul>
    <li>SerialNumber: (long - required)</li>
    <ul>
      <li>Logger Serial number as dispalyed on device</li>
    </ul>
    <li>StartDate: (string - yyyy-MM-dd HH:mm)</li>
    <ul>
      <li>Date at which to start querying loggers channel data</li>
    </ul>
    <li>EndDate: (string - yyyy-MM-dd HH:mm)</li>
    <ul>
      <li>Date at which to finish querying loggers channel data. (No more than 8 days after start date) </li>
    </ul>
    <li>Token: (string - required)</li>
    <ul>
      <li>Access token</li>
    </ul>
  </ul>
</li>
</ol>
<h3>Return Value</h3>
An object containing meta data for channel:
<pre>
{
   channelName: string,
   dailyStats: [{
	date: datetime,
	minTime: dateTime,
	maxTime: dateTime,
	minValue: number,
          maxValue: number,
	totaliser: number
    }]
}

</pre>
<h3>Example</h3>
