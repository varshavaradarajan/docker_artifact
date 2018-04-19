require 'erb'

def get_var(name)
  if ENV[name].to_s.strip.empty?
    raise "environment #{name} not specified!"
  else
    ENV[name]
  end
end

username = get_var('DOCKERHUB_USERNAME')
go_pipeline_label = get_var('GO_PIPELINE_LABEL')

task :create_docker_image do
  sh("docker build . -t #{username}/artifact_demo:#{go_pipeline_label}")
end

task :create_json do
  template = File.read('artifact_info.json.erb')
  renderer = ERB.new(template, nil, '-')
  File.open('artifact_info.json', 'w') do |f|
    f.puts(renderer.result(binding))
  end
end