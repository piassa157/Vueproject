<template>
	<div>
		<div id="main">
			<div class="container">
				<div class="row">
					<div class="col-md">
						<putDomains title="Prefixes" v-bind:items="prefixes" v-on:addItem="addPrefix" v-on:deleteItem="deletePrefix"></putDomains>
					</div>
					<div class="col-md">
						<putDomains title="Sufixes" v-bind:items="sufixes" v-on:addItem="addSufix" v-on:deleteItem="deleteSufix"></putDomains>
					</div>
				</div>
				<br/>
				<h5>Domains <span class="badge badge-info">{{ domains.length }}</span></h5>
				<div class="card">
					<div class="card-body">
						<ul class="list-group">
							<li class="list-group-item" v-for="domain in domains" v-bind:key="domain.name">
								<div class="row">
									<div class="col-md">
										{{ domain.name }}
									</div>
									<div class="col-md text-right">
										<a class="btn btn-info" v-bind:href="domain.checkout" target="_blank">
											<span class="fa fa-shopping-cart"></span>
										</a>
									</div>
								</div>
							</li>
						</ul>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "font-awesome/css/font-awesome.css";
import putDomains from "./putDomains";
export default {
	name: "app",
	components: {
		putDomains
	},
	data: function () {
		return {
			prefixes: ["Air", "Jet", "Flight"],
			sufixes: ["Hub", "Station", "Mart"]
		};
	},
	methods: {
		addPrefix(prefix) {
			this.prefixes.push(prefix);
		},
		deletePrefix(prefix) {
			this.prefixes.splice(this.prefixes.indexOf(prefix), 1);
		},
		addSufix(sufix) {
			this.sufixes.push(sufix);
		},
		deleteSufix(sufix) {
			this.sufixes.splice(this.sufixes.indexOf(sufix), 1);
		}
	},
	computed: {
		domains() {
			console.log("generating domains...");
			const domains = [];
			for (const prefix of this.prefixes) {
				for (const sufix of this.sufixes) {
					const name = prefix + sufix;
					const url = name.toLowerCase();
					const checkout = `https://checkout.hostgator.com.br/?a=add&sld=${url}&tld=.com.br`;
					domains.push({
						name,
						checkout
					});
				}
			}
			return domains;
		}
	}
};
</script>

<style>
#main {
	background-color: #f1f1f1;
	padding-top: 30px;
	padding-bottom: 30px;
    border-radius: 15px;
    padding-left: 30px;
    padding-right: 30px;
}

</style>