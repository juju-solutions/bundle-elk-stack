# Logstash Core - subject to renaming

The Elastic Stack — that's Elasticsearch, Logstash, Kibana, and Beats — are open
source projects that help you take data from any source, any format and search,
analyze, and visualize it in real time.

## The Elastic Stack

**Elasticsearch** is a distributed, open source search and analytics engine, designed for horizontal scalability, reliability, and easy management. It combines the speed of search with the power of analytics via a sophisticated, developer-friendly query language covering structured, unstructured, and time-series data.

**Logstash** is a flexible, open source data collection, enrichment, and transportation pipeline. With connectors to common infrastructure for easy integration, Logstash is designed to efficiently process a growing list of log, event, and unstructured data sources for distribution into a variety of outputs, including Elasticsearch.

**Kibana** is an open source data visualization platform that allows you to interact with your data through stunning, powerful graphics. From histograms to geomaps, Kibana brings your data to life with visuals that can be combined into custom dashboards that help you share insights from your data far and wide.


This bundle is a 4 node cluster designed to scale out.
Built around Elastic components, it contains:

- 1 Logstash unit (minimum mem=2GB)
- 2 Elasticsearch units
- 1 Kibana unit

## Usage

    juju deploy ~containers/bundle/logstash-core

## Testing the deployment

The services provide extended status reporting to indicate when they are ready:

    uju status --format=tabular

This is particularly useful when combined with watch to track the on-going progress of the deployment:

    watch -n 0.5 juju status --format=tabular

The message for each unit will provide information about that unit's state.
Once they all indicate that they are ready, you can use the provided
`generate-noise` action to test that the Elastic Stack components are working
as expected:

    juju action do logstash/0 generate-noise
    watch juju action status

Once the action is complete, you can retrieve the results:

    juju action fetch <action-id>

The &lt;action-id&gt; value will be in the juju action status output.

## Scale Out Usage

This bundle was designed to scale out. To increase the amount of log storage and indexers, you can add-units to elasticsearch.

    juju add-unit elasticsearch

You can also increase in multiples, for example: To increase the number of logstash parser/shipping services:

    juju add-unit -n 2 logstash


## Contact information

- Charles Butler &lt;charles.butler@canonical.com&gt;
- Matt Bruzek &lt;matthew.bruzek@canonical.com&gt;

# Need Help?

- [Juju mailing list](https://lists.ubuntu.com/mailman/listinfo/juju)
- [Juju Community](https://jujucharms.com/community)
