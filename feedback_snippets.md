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
