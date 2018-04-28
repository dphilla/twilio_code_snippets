## Snippets for drafting of Twilio ASR Blog Post


### page 6

```ruby
get '/messages', to: 'twilio#index'
```

```ruby
class TwilioController < ApplicationController
skip_before_action :verify_authenticity_token

 def index

 end

end
```


### page 7

```xml
<Response>
  <Gather action="/messages" input="speech" method="POST" timeout="2">
    <Say>What is your message for Daniels Banana Cabana?</Say>
  </Gather>
</Response>
```


### page 8

```ruby
class TwilioService
  def initialize
  end

  def get_speech
  end

  def say_goodbye
  end
end
```

```ruby
  def initialize
    @reponse = Twilio::TwiML::VoiceResponse.new
  end
```

```ruby
  def get_speech
    @reponse.gather(input: 'speech', timeout: 2, action: '/messages', method: 'POST') do |gather|
      gather.say('What is your message for Daniels Banana Cabana?')
    end
  end
```

```ruby
  def index
    @speech = TwilioService.new.get_speech
    render :xml => @speech
  end
```

### page 9


```xml
<Response>
  <Gather action="/messages" input="speech" method="POST" timeout="2">
    <Say>What is your message for Daniels Banana Cabana?</Say>
  </Gather>
</Response>
```

```ruby
post '/messages', to: 'twilio#create'
```

```ruby
  def create

  end
```

### page 10

```ruby
  def create
    binding.pry
  end
```

```bash
pry(#<TwilioController>)>
```

```bash
pry(#<TwilioController>)> params['SpeechResult']
=> "This is a test message."
```

```bash
pry(#<TwilioController>)> params['Confidence']
=> "0.83758247"
```

### page 11

```ruby
  def create
    if params['SpeechResult']
      asr_message = params['SpeechResult']
      asr_caller = params['Caller']
      Message.create(caller: asr_caller, body: asr_message)
    end
  end
```

### page 12

```ruby
  def say_goodbye
    @response.say('Thank you, this call will now end')
    @reponse.hangup
  end
```

```ruby
  def create
    if params['SpeechResult']
      asr_message = params['SpeechResult']
      asr_caller = params['Caller']
      Message.create(caller: asr_caller, body: asr_message)
    end
    @speech = TwilioService.new.say_goodbye
    render :xml => @speech
  end
```

```ruby
get '/inbox', to: 'inbox#index'
```

```ruby
class InboxController < ApplicationController
  def index
    @messages = Message.all
  end
end
```
