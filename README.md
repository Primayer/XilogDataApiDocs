<h1> Xilog API documentation </h1>
Questions? Find us at <a href=mailto:development@ovarro.com> development@ovarro.com </a>

<h1> Xilog Data Access </h1>
The Xilog API provides access to the raw data recorded by the Xilog logger. To use the API third parties must provide an authorization token with each request. At the moment this API only supports the 4G variant of Xilog.

# Methods 
- [*Logger/All*](#loggeralltoken): Returns all loggers for the access token</li>
- [*Data/All*](#dataallserialnumberstartdateenddatetoken): Returns all data for logger for the specified date range</li>
- [*Data/Channel*](#datachannelserialnumberchannelnamestartdateenddatetoken): Returns all data for logger for the specified channel and date range</li>
- [*Data/DailyStats*](#datadailystatsserialnumberstartdateenddatetoken): Returns statistical data on each channel for the specified date range.</li>

# API
## Logger/All/{token}
#### Purpose
Returns array of loggers for the access token
#### Signature
<ol>
<li>Endpoint : https://app-loggervision-logger-prod-uks-001.azurewebsites.net/Logger/All
</li>
<li> Params </li>
  <ul>
    <li>Token: (string - required)</li>
    <ul>
      <li>Access token</li>
    </ul>
  </ul>

</ol>

#### Return Value
An array of loggers containing serial number and name.
<pre>
[{
  serial: number,
  name: string
}]
</pre>

#### Example

https://app-loggervision-logger-prod-uks-001.azurewebsites.net/Logger/All/00000000-0000-0000-0000-000000000000

Example Output:
<pre>
[
  {
    "serial":12345678,
    "name":"12345678"
  },
  {
    "serial":ABCDEFGH,
    "name":"ABCDEFGH"
  }
]
</pre>

## Data/All/{SerialNumber}/{StartDate}/{EndDate}/{Token}
#### Purpose
Returns a collection of the raw channel data for the specified Xilog 4g logger. (Max 8 days)
#### Signature
<ol>
<li>Endpoint : <a href="https://app-loggervision-logger-prod-uks-001.azurewebsites.net/Data/All/"> https://app-loggervision-logger-prod-uks-001.azurewebsites.net/Data/All/</a>
</li>
<li> Params </li>
  <ul>
    <li>SerialNumber: (long - required)</li>
    <ul>
      <li>Logger Serial number as displayed on device</li>
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
</ol>

#### Return Value
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

#### Example

https://app-loggervision-logger-prod-uks-001.azurewebsites.net/Data/All/12345678/2021-08-05%2003:30/2021-08-05%2003:40/00000000-0000-0000-0000-000000000000

Example Output:
<pre>
[
  {
    "channelName":"Flow 1",
    "data":[
      {
        "type":8,
        "data":[
	  {
	    "timestamp":"2021-08-05T03:30:30Z",
	    "value":0
	  },
	  {
	    "timestamp":"2021-08-05T03:31:30Z",
	    "value":0
	  },
	  {
	    "timestamp":"2021-08-05T03:32:30Z",
	    "value":0
	  },
	  …
          {
	    "timestamp":"2021-08-05T03:38:30Z",
	    "value":0
	  },
	  {
	    "timestamp":"2021-08-05T03:39:30Z",
	    "value":0
	  }
	]
      }
    ]
  },
  {
    "channelName":"Flow 2",
    "data":[
      {
        "type":8,
	"data":[
	  {
	    "timestamp":"2021-08-05T03:30:30Z",
 	    "value":0 
	  },
	  …
	  {
	    "timestamp":"2021-08-05T03:39:30Z",
	    "value":0
	  }
        ]
      }
    ]
  }
]

</pre>

## Data/Channel/{SerialNumber}/{ChannelName}/{StartDate}/{EndDate}/{Token})
#### Purpose
Returns a collection of the raw data for the specified Xilog 4g logger and channel name. (Max 8 days)
#### Signature
<ol>
<li>Endpoint : <a href=" https://app-loggervision-logger-prod-uks-001.azurewebsites.net/Data/Channel/">https://app-loggervision-logger-prod-uks-001.azurewebsites.net/Data/Channel/</a>
</li>
<li> Params </li>
  <ul>
    <li>SerialNumber: (long - required)</li>
    <ul>
      <li>Logger Serial number as displayed on device</li>
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

#### Example

https://app-loggervision-logger-prod-uks-001.azurewebsites.net/Data/Channel/12345678/Flow%201/2021-08-05%2003:30/2021-08-05%2003:40/00000000-0000-0000-0000-000000000000

Example Output:

<pre>
[
  {
    "channelName":"Flow 1",
    "data":[
      {
        "type":8,
	"data":[
	  {
	    "timestamp":"2021-08-05T03:30:30Z",
	    "value":0
          },
          {
      	     "timestamp":"2021-08-05T03:31:30Z",
             "value":0
          },
	  {
	     "timestamp":"2021-08-05T03:32:30Z",
	     "value":0
	  },
	  …
	  {
	     "timestamp":"2021-08-05T03:38:30Z",
	     "value":0
	  },
	  {
	     "timestamp":"2021-08-05T03:39:30Z",
	     "value":0
	  }
        ]
      }
    ]
  }
]
</pre>

## Data/DailyStats/{SerialNumber}/{StartDate}/{EndDate}/{Token}
#### Purpose
Returns the daily data statistics for the serial number and specified date. 
#### Signature
<ol>
<li>Endpoint : <a href=" https://app-loggervision-logger-prod-uks-001.azurewebsites.net/Data/DailiyStats/">  https://app-loggervision-logger-prod-uks-001.azurewebsites.net/Data/DailiyStats/</a>
</li>
<li> Params </li>
  <ul>
    <li>SerialNumber: (long - required)</li>
    <ul>
      <li>Logger Serial number as displayed on device</li>
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

</ol>

#### Return Value
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
#### Example

https://app-loggervision-logger-prod-uks-001.azurewebsites.net/Data/DailyStats/12345678/2021-08-15/2021-08-16/00000000-0000-0000-0000-000000000000

<pre>
{
  "channelName": "Flow 1",
  "dailyStats": [
    {
      "date": "2021-08-15T00:00:00Z",
      "minTime": "2021-08-15T00:01:00",
      "maxTime": "2021-08-15T00:00:00",
      "minValue": 0,
      "maxValue": 0,
      "totaliser": 0
    },
    {
      "date": "2021-08-16T00:00:00Z",
      "minTime": "2021-08-16T00:01:00",
      "maxTime": "2021-08-16T00:00:00",
      "minValue": 0,
      "maxValue": 0,
      "totaliser": 0
    }
  ],
}

</pre>
