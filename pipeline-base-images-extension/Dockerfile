FROM ibmcom/pipeline-base-image:latest

# https://www.vultr.com/docs/installing-docker-ce-on-ubuntu-16-04
# Step 1 and step 2
RUN apt-get update && \
    apt-get install -y apt-transport-https ca-certificates curl software-properties-common
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

# Step 3 and additional step - add complementary tools (nc)
RUN apt-get update && \
    apt-get install -y docker-ce netcat jq build-essential && \
    apt-get -q clean && \
    rm -rf /var/lib/apt/lists 

# Trust the certificates to be able to connect to the exchange
copy horizon-cli.crt /usr/local/share/ca-certificates
copy icp.crt /usr/local/share/ca-certificates
RUN update-ca-certificates

# Add the horizon cli
copy horizon-cli_2.23.29~ppa~ubuntu.bionic_amd64.deb ./
#copy horizon_2.23.29~ppa~ubuntu.bionic_amd64.deb ./
#copy bluehorizon_2.23.29~ppa~ubuntu.bionic_all.deb ./
RUN dpkg -i horizon-cli_2.23.29~ppa~ubuntu.bionic_amd64.deb 

# Install pre-reqs for getting the horizon pkgs
# RUN apt-get update && apt-get upgrade -y && apt-get install -y curl vim jq wget apt-transport-https software-properties-common gettext-base psmisc gnupg

