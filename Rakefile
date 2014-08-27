require 'rubygems'
require 'bundler/setup'
require 'yaml'
require 'faraday'

namespace :seevogh do
  task :config do
    CONFIG = YAML.load_file('config.yml')
    API_URL = 'https://seevogh.com/'
    API_PATH = 'api/meeting/create'
  end

  desc "Create seevogh meeting"
  task :create => :config do
    conn = Faraday.new(url: API_URL) do |faraday|
      faraday.request  :url_encoded             # form-encode POST params
      faraday.response :logger                  # log requests to STDOUT
      faraday.adapter  Faraday.default_adapter  # make requests with Net::HTTP
    end

    resp = conn.post API_PATH, {
      "apiLogin" => CONFIG['login'],
      "apiPassword" => CONFIG['password'],
      "meetingPwd" => "RCS2014-mod",
      "meetingName" => "Recurring-test",
      "meetingType" => 0,
      "meetingDuration" => 1,
      "meetingNbrParticipants" => 10,
      "meetingQuality" => 3,
      "meetingAccessCode" => "RCS2014",
      "optionRecording" => 1,
      "optionH232sip" => 3,
      "optionAudio" => 4,
      "optionVideo" => 4,
      "optionAlias" => "RecurringTest"
    }

    puts resp.body
  end
end
