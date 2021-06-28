# xgt-ruby Recipes

### Monitor a seed nodes notion of HEAD
```ruby
def head_block_number
  res = rpc.call('database_api.get_dynamic_global_properties',{})
  res["head_block_number"]
end

next_block = head_block_number
while true do
  sleep(0.25)
  res = rpc.call('block_api.get_block', { 'block_num' => next_block }); bid = (res["block"] || {})["block_id"]
  p bid
  if bid.nil?; sleep 1; redo; end
  p next_block += 1
end

```

### Generate checkpoints for config.ini
```ruby
def get_checkpoint(block_num)
  res = rpc.call('block_api.get_block', { 'block_num' => block_num })
  block_id = res["block"]["block_id"]
  "checkpoint = [#{block_num}, \"#{block_id}\"]"
end

def head_block_number
  res = rpc.call('database_api.get_dynamic_global_properties',{})
  res["head_block_number"]
end

def generate_checkpoints
  period_length = 20_000

  periods = head_block_number / period_length

  remainder = head_block_number % period_length

  check_count = 8

  points = []

  check_count.times do |i|
    points << head_block_number - (remainder /= 2)
  end

  periods.times do |period|
    block_num = (period + 1) * period_length
    puts get_checkpoint(block_num)
  end

  points.map do |block_num|
    next if block_num > head_block_number
    puts get_checkpoint(block_num)
  end
end

```

### Block production rate
Get block production statistics, emits TSV useful for offline analysis.
```ruby

def head_block_number
  res = rpc.call('database_api.get_dynamic_global_properties',{})
  res["head_block_number"]
end

def model_bp_rate
  hbn = head_block_number


  periods = hbn / 10_000
  x = 1
  until x > hbn
    x += 10_000
    res = rpc.call('block_api.get_block', { 'block_num' => x })
    ts = Time.parse(res["block"]["timestamp"]).strftime("%m/%d/%Y %H:%M")
    puts "#{ts}\t#{x}"
  end

end
```
